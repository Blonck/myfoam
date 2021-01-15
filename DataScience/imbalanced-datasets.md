# Handling Imabalanced datassets

## Over sample/under sample underrepresented class

```python
trainset["TRAIN"] = False
trainset.loc[cv_set[0][0], "TRAIN"] = True
    
assert not trainset.loc[cv_set[0][1], "TRAIN"].any()
    
train_t = trainset[trainset.TRAIN]
val = trainset[~trainset.TRAIN]
    
churned = train_t[train_t['LABEL'] == 1.0]
stay = train_t[train_t['LABEL'] == 0.0]
# undersampling
#stay = stay.sample(n=3 * churned.shape[0], random_state=42)
# oversampling
#churned = churned.sample(n=stay.shape[0], replace=True, random_state=42)
trainset = pd.concat([churned, stay])
```
 
 ### Links
 * [https://imbalanced-learn.readthedocs.io/en/stable/api.html]

## Weight samples

### pytorch

```python
# weight per class
weight = trainset.shape[0] / trainset['LABEL'].value_counts()
l2w = {i[0]: i[1] for i in weights.iteritems()}
# weight per row
weight_trainset = trainset['LABEL'].map(l2w)	
	
loss = CrossEntropyLossFlat(weight=torch.tensor(weight).float().cuda())
```

### sklearn
 
 * random forest -> class balanced

## Use loss which handles imbalanced datassets

### pytorch

```python
class FocalLoss(nn.Module):
    def __init__(self, gamma=2):
        super().__init__()
        self.gamma = gamma

    def forward(self, logit, target):
        target = target.float()
        max_val = (-logit).clamp(min=0)
        loss = logit - logit * target + max_val + \
               ((-max_val).exp() + (-logit - max_val).exp()).log()

        invprobs = F.logsigmoid(-logit * (target * 2.0 - 1.0))
        loss = (invprobs * self.gamma).exp() * loss
        if len(loss.size())==2:
            loss = loss.sum(dim=1)
        return loss.mean()
```

## Links

* [https://imbalanced-learn.org/stable/] 
* [https://www.kaggle.com/c/human-protein-atlas-image-classification/discussion/78109]
* [https://medium.com/analytics-vidhya/augment-your-data-easily-with-pytorch-313f5808fc8b]
* [https://medium.com/@champs.jaideep/stratified-batch-sampler-using-fastai-20f9b898609d]
* [https://forums.fast.ai/t/highly-imbalanced-data/37001/4]
* [https://forums.fast.ai/t/highly-imbalanced-data/37001/14]