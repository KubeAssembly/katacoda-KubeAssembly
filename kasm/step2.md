`wget -q https://raw.githubusercontent.com/dapr/cli/master/install/install.sh -O - | /bin/bash`{{execute}}

`dapr init --kubernetes --wait`{{execute}}

`dapr status -k`{{execute}}
