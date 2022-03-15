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
