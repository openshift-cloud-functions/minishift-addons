# OCF minishift addons

After cloning this repo locally, install its addons:

    $ minishift addons install minishift-addons/istio
    $ minishift addons install minishift-addons/knative

With minishift running, install istio with its addon:

    $ minishift addons apply istio

When this command completes, istio is ready:

    $ while oc get pods -n istio-system | grep -v -E "(Running|Completed|STATUS)"; do sleep 5; done

Now install knative with its addon:

    $ minishift addons apply knative

When this command completes, knative is ready:

    $ while oc get pods -n knative-serving | grep -v -E "(Running|Completed|STATUS)"; do sleep 5; done
