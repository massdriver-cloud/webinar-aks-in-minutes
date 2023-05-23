# Ruby on Rails 7 Demo on Kubernetes

This runs a demo of the e-commerce platform Spree using the `rails-kubernetes` application template.

**Links:**

* [Rails Kubernetes Application Template](https://github.com/massdriver-cloud/application-templates/tree/main/rails-kubernetes)
* [Spree Starter Example App Source Code](https://github.com/massdriver-cloud/spree_starter)
* [Example Spree App Bundle Source Code](https://github.com/massdriver-cloud/webinar-aks-in-minutes/tree/main/deploy)
## Setup

The admin email and password can be set via secrets added on this bundle:

* `ADMIN_EMAIL`
* `ADMIN_PASSWORD`

To setup the example database, `kubectl exec` into a Rails/Spree pod and run.

You can find your package name by following the docs [here](https://docs.massdriver.cloud/applications/deploying-application#:~:text=expects%20the%20package%20name).

```shell
export MD_PACKAGE_NAME=YOUR_NAME
kubectl exec $(kubectl get pod -l md-package=${MD_PACKAGE_NAME} -o jsonpath="{.items[0].metadata.name}") -it -- /bin/bash
```

Run the following commands to create admin user and sample data.

```shell
bundle exec rake db:seed
bundle exec rake spree_sample:load
```

To log into the admin page, visit: `https://YOUR_SITE.com/admin`

The [legacy frontend](https://github.com/spree/spree_legacy_frontend) is not configured.
