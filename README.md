# Amazon EKS Container Networking Workshop

### Setup:

#### Install Hugo:
On a Mac:

`brew install hugo`

On Linux:
  - Download from the releases page: https://github.com/gohugoio/hugo/releases/tag/v0.46
  - Extract and save the executable to `/usr/local/bin`

#### Clone this repo:
From wherever you checkout repos:
`git clone https://github.com/aws-samples/amazon-eks-and-amazon-ec2-k8s-container-networking-workshops`

#### Clone the theme submodule:
`cd cont-net-ws-staging`

```bash
pushd themes/learn
git submodule init
git submodule update --checkout --recursive
popd
```
Run hugo to generate the site, and point your browser to http://localhost:1313

```bash
hugo serve -D
```


