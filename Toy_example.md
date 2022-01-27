# Toy example

## MNIST
### 网络结构
```
self.encoder = nn.Sequential(
                nn.Linear(784, self.hidden_size),
                nn.ReLU(),
                nn.Linear(self.hidden_size, self.hidden_size),
                nn.ReLU(),
                )
self.fc_mu = nn.Linear(self.hidden_size, self.latent_dim)
self.fc_var = nn.Linear(self.hidden_size, self.latent_dim)

self.reparameterize

self.decoder = nn.Sequential(
            nn.Linear(self.latent_dim, self.hidden_size),
            nn.ReLU(),
            nn.Linear(self.hidden_size, self.hidden_size),
            nn.ReLU(),
            nn.Linear(self.hidden_size, 784),
            nn.Sigmoid(),
            )
```
### 正常数据训练
> 60000 (55000/5000), balanced

recon
<img src="figure/recon.png" alt="recons" style="zoom: 66%;" />
sample
<img src="figure/sample.png" alt="sample" style="zoom: 66%;" />

### 少量数据训练
> Two complete classes, balanced

recon
<img src="figure/recon_01.png" alt="recons01" style="zoom: 66%;" />
sample
<img src="figure/sample_01.png" alt="sample01" style="zoom: 66%;" />

recon
<img src="figure/recon_17.png" alt="recons17" style="zoom: 66%;" />
sample
<img src="figure/sample_17.png" alt="sample17" style="zoom: 66%;" />

> One complete class

recon
<img src="figure/recon_2.png" alt="recons2" style="zoom: 66%;" />
sample
<img src="figure/sample_2.png" alt="sample2" style="zoom: 66%;" />

> One class with 100 samples

recon
<img src="figure/recon_2_100.png" alt="recons2_100" style="zoom: 66%;" />
sample
<img src="figure/sample_2_100.png" alt="sample2_100" style="zoom: 66%;" />

> One class with 50 samples

recon
<img src="figure/recon_2_50.png" alt="recons2_50" style="zoom: 66%;" />
sample
<img src="figure/sample_2_50.png" alt="sample2_50" style="zoom: 66%;" />

> One class with 5 samples

recon
<img src="figure/recon_2_5.png" alt="recons2_5" style="zoom: 66%;" />
sample
<img src="figure/sample_2_5.png" alt="sample2_5" style="zoom: 66%;" />


## Celeba
