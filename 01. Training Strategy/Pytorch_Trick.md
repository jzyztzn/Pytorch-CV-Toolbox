## PyTorch trick: Lazy layers

When we deal with pre-trained models, we have to replace the final linear layer with something suitable for the data we are working with. 
A lot of public notebooks do something like this:

  ```
  self.model = timm.create_model(self.cfg.model_name, pretrained=pretrained)
  self.n_features = self.model.classifier.in_features
  self.model.classifier = nn.Identity()
  self.fc = nn.Linear(self.n_features, self.cfg.target_size)
  ```

The downside of this is that if you change model architecture (e.g. from EfficientNet to a ResNet), this may break, since the linear layer may have a different name.
An easy way to do this in an architecture agnostic manner is to use LazyLinear:

  ```
  self.model = timm.create_model(self.cfg.model_name, pretrained=True, num_classes=0)
  self.fc = nn.LazyLinear(self.cfg.target_size)
  ```
What's going on here?

  1) num_classes=0 tells timm to return a pooled feature vector. The size of this vector can vary between architectures (e.g. 512 for ResNet34 or 1280 for EfficientNet-B0)
  LazyLinear will determine what the input size is and create a normal linear layer accordingly
  2) This allows us to quickly switch architectures (e.g. in a config file) without changing code. 




## Concat Multi Dataset
PyTorch provides a torch.utils.data.ConcatDataset capable of connecting several different data sets. This class is useful to assemble different existing datasets.
```
from torchvision.datasets import MNIST
from torchvision.datasets import CIFAR100
from torch.utils.data import ConcatDataset

import numpy as np

if __name__ == "__main__":
    mnist_data = MNIST('./data', train=True, download=True)
    print('mnist: ', len(mnist_data))
    cifar10_data = CIFAR100('./data', train=True, download=True)
    print('cifar: ', len(cifar10_data))

    concat_data = ConcatDataset([mnist_data, cifar10_data])
    print('concat_data: ', len(concat_data))

    img, target = concat_data.__getitem__(133)
    print(np.array(img).shape)
    print(target)

    ##  output
    # mnist:  60000
    # Files already downloaded and verified
    # cifar:  50000
    # concat_data:  110000
    # (28, 28)
    # 9 

```


