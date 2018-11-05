# OCF minishift addons

After cloning this repo locally, install its addons:

    $ minishift addons install minishift-addons/istio
    $ minishift addons install minishift-addons/knative
    $ minishift addons install minishift-addons/knative-eventing

First, install istio. This could take a few minutes, but once it
completes you should see a number of running pods in the
`istio-system` namespace.

    $ minishift addons apply istio

Once that completes, install knative (both build, serving and eventing):

    $ minishift addons apply knative
    $ minishift addons apply knative-eventing

