# openshift-bluegreen-nginx

Commands ran in demo:

helm install -n polybius --create-namespace=true ocp-nginx-bluegreen . --set blue.timestamp="$(date '+%Y-%m-%d %H:%M:%S')" --set blue.enabled=true --set blue.weight=100
curl https://production-deployment-friday.apps.cluster-v879j.v879j.sandbox1667.opentlc.com
helm upgrade -n polybius ocp-nginx-bluegreen . --reuse-values --set green.enabled=true --set green.timestamp="$(date '+%Y-%m-%d %H:%M:%S')" --set green.weight=0 --debug
curl https://production-deployment-friday.apps.cluster-v879j.v879j.sandbox1667.opentlc.com
helm upgrade -n polybius ocp-nginx-bluegreen . --reuse-values --set blue.weight=0 --set green.weight=100
curl https://production-deployment-friday.apps.cluster-v879j.v879j.sandbox1667.opentlc.com
