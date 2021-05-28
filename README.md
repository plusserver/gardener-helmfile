# gardener-helmfile

Deployment of gardener with the helm charts via helmfile.

**This will not deploy a functional gardener setup**, it is only a reference for the minimal set of values needed when deploying gardener with the helm charts.

**Don’t run this on clusters exposed to the internet**

## Usage

You need to have the following installed:

* helmfile
* helm
* helm-git

You need to have a kubectl context `garden` and a context `seed` for the garden and seed clusters respectively.

Run

```sh
git clone https://github.com/gardener/gardener.git /tmp/gardener
```

Export the required environment variables (check `seed.yaml` and `garden.yaml`).
In this deployment, AWS Route53 is used for DNS, so you need to specify valid AWS access credentials with write access to your `BASE_DOMAIN` zone. `BASE_DOMAIN` does not need to be a top-level domain.

Then, run `helmfile diff` and `helmfile apply` if you’re happy with the diff.

If you want to use this to deploy a fully functional setup, you need to:

* Deploy the needed controller registrations for your environment
* Deploy a bootstrap token for the gardenlet to the garden cluster and set it in line 37 of seed.yaml.
* Deploy CloudProfiles to use with the configured seed
