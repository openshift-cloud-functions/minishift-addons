# OCF minishift addons

After cloning this repo locally, install your desired addons:

    $ minishift addons install minishift-addons/knative-istio
    $ minishift addons install minishift-addons/knative-build
    $ minishift addons install minishift-addons/knative-serving
    $ minishift addons install minishift-addons/knative-eventing

All of the addons use the `KNATIVE_VERSION` environment variable to
indicate which release is to be installed. The default (and probably
minimum supported) is `v0.2.1`.

    $ minishift config set addon-env KNATIVE_VERSION=v0.2.1

Knative components require istio, and the `knative-istio` addon
contained in this repo applies the manifest published in official
upstream knative repos.

    $ minishift addons apply knative-istio

Once that completes, install the knative resources you desire:

    $ minishift addons apply knative-build
    $ minishift addons apply knative-serving
    $ minishift addons apply knative-eventing

To use knative, i.e. create and manipulate its custom resources (CRs),
you'll need the appropriate permissions in your project/namespace. For
example:

    $ oc adm policy add-scc-to-user anyuid -z default -n myproject
    $ oc adm policy add-scc-to-user privileged -z default -n myproject
