# OCF minishift addons

### Install

After cloning this repo locally, install your desired addons:

    $ minishift addons install minishift-addons/knative-istio
    $ minishift addons install minishift-addons/knative-build
    $ minishift addons install minishift-addons/knative-build-pipeline
    $ minishift addons install minishift-addons/knative-serving
    $ minishift addons install minishift-addons/knative-eventing

### Apply

Knative requires Istio, and the `knative-istio` addon
contained in this repo applies the manifest published in the
upstream knative-serving repo.

    $ minishift addons apply knative-istio

Once that completes, install the knative resources you desire:

    $ minishift addons apply knative-build
    $ minishift addons apply knative-build-pipeline
    $ minishift addons apply knative-serving
    $ minishift addons apply knative-eventing

To use knative, i.e. create and manipulate its custom resources (CRs),
you'll need the appropriate permissions in your project/namespace. For
example:

    $ oc adm policy add-scc-to-user anyuid -z default -n myproject
    $ oc adm policy add-scc-to-user privileged -z default -n myproject

### Remove

You can remove the resources created by each addon like so:

    $ minishift addons remove knative-build
    $ minishift addons remove knative-build-pipeline
    $ minishift addons remove knative-serving
    $ minishift addons remove knative-eventing
    $ minishift addons remove knative-istio

### Uninstall

And you can uninstall the addons thusly:

    $ minishift addons uninstall knative-build
    $ minishift addons uninstall knative-build-pipeline
    $ minishift addons uninstall knative-serving
    $ minishift addons uninstall knative-eventing
    $ minishift addons uninstall knative-istio

Upgrading an addon typically amounts to uninstalling it, and then
installing the new one.

### Versions

Though we try to keep the defaults set to the latest stable version,
each addon may be optionally configured with any older version you
wish to install by setting an addon environment variable. For example,

    $ minishift addons apply --addon-env KNATIVE_BUILD_VERSION=v0.2.0 knative-build
    $ minishift addons apply --addon-env KNATIVE_BUILD_PIPELINE_VERSION=previous/v20181204-559397d7-dirty knative-build-pipeline
    $ minishift addons apply --addon-env KNATIVE_SERVING_VERSION=v0.2.2 knative-serving
    $ minishift addons apply --addon-env KNATIVE_EVENTING_VERSION=v0.2.0 knative-eventing

You should be careful when removing an addon to specify the same
version you used when you applied it.
