# PyTorch Lighting trick
When we want to add some custom config in Trainer, we can use the parameter "callbacks"

## Learnint rate
Use LearningRateMonitor monitors how the learning rate changes.


```
import pytorch_lightning as pl
from pytorch_lightning.callbacks import LearningRateMonitor
 
lr_monitor = LearningRateMonitor(logging_interval='step')
 
trainer = pl.Trainer(gpus=ngpus_per_node,
                     callbacks=[..., lr_monitor],
                         ...)
```

## LitProgressBar
If the progress bar refreshes too quickly, it causes the progress bar to fill the screen, we can use LitProgressBar.

```
import sys
class LitProgressBar(pl.callbacks.TQDMProgressBar):
    def init_sanity_tqdm(self) -> tqdm:
        """ Override this to customize the tqdm bar for training. """
        bar = tqdm(
            desc='Sanity',
            initial=self.train_batch_idx,
            position=(2 * self.process_position),
            disable=self.is_disabled,
            leave=True,
            dynamic_ncols=False,  # This two lines are only for pycharm
            ncols=100,
            file=sys.stdout,
            smoothing=0,
        )
        return bar
    
    def init_train_tqdm(self) -> tqdm:
        """ Override this to customize the tqdm bar for training. """
        bar = tqdm(
            desc='Training',
            initial=self.train_batch_idx,
            position=(2 * self.process_position),
            disable=self.is_disabled,
            leave=True,
            dynamic_ncols=False,  # This two lines are only for pycharm
            ncols=100,
            file=sys.stdout,
            smoothing=0,
        )
        return bar

    def init_validation_tqdm(self) -> tqdm:
        """ Override this to customize the tqdm bar for validation. """
        # The main progress bar doesn't exist in `trainer.validate()`
        has_main_bar = self.main_progress_bar is not None
        bar = tqdm(
            desc='Validating',
            position=(2 * self.process_position + has_main_bar),
            disable=self.is_disabled,
            leave=False,
            dynamic_ncols=False,
            ncols=100,
            file=sys.stdout
        )
        return bar

    def init_test_tqdm(self) -> tqdm:
        """ Override this to customize the tqdm bar for testing. """
        bar = tqdm(
            desc="Testing",
            position=(2 * self.process_position),
            disable=self.is_disabled,
            leave=True,
            dynamic_ncols=False,
            ncols=100,
            file=sys.stdout
        )
        return bar

    def init_predict_tqdm(self) -> tqdm:
        """ Override this to customize the tqdm bar for testing. """
        bar = tqdm(
            desc="Predicting",
            position=(2 * self.process_position),
            disable=self.is_disabled,
            leave=True,
            dynamic_ncols=False,
            ncols=100,
            file=sys.stdout
        )
        return bar


litprograssbar = LitProgressBar()
trainer = pl.Trainer(gpus=ngpus_per_node,
                     callbacks=[..., litprograssbar],
                         ...)

```

## Stochastic Weight Averaging
There are two ways to add swa

1. Add default config, only open the Trainer flag.

```
trainer = pl.Trainer(gpus=ngpus_per_node,
                     stochastic_weight_avg=True,
                         ...)
```

2. add custom config.
```
swa_callback = pl.callbacks.StochasticWeightAveraging(
        swa_epoch_start=0.9, 
        swa_lrs=None, 
        annealing_epochs=4, 
        annealing_strategy='cos', 
        avg_fn=None)
trainer = pl.Trainer(gpus=ngpus_per_node,
                     callbacks=[..., swa_callback],
                         ...)


```

## Save model

By default, only the last model is saved. If we want to save multiple models during training.

1. Save the top3 models.
```
from pytorch_lightning.callbacks import ModelCheckpoint
checkpoint_callback = ModelCheckpoint(
	monitor="val_loss",
	dirpath=save_path,
	filename="your model name" + "-{epoch:02d}-{val_loss:2.2f}",
	save_top_k=3,
	mode="min",
)
trainer = pl.Trainer(gpus=ngpus_per_node,
                     callbacks=[..., checkpoint_callback],
                         ...)


```
