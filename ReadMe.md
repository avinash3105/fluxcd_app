flux bootstrap github \
--token-auth \
--owner=$GITHUB_USER \
--repository=fluxcdtest \ 
--branch=main \
--path=email-dev \
--personal


#Define Source of Truth
flux create source git fluxcdapp \
--url=https://github.com/avinash3105/fluxcdapp.git \
--branch=main \
--interval=30s \
--export > ./deploy/flux_source2.yaml

#Apply above source SOT using kustomization controller
flux create kustomization fluxcdapp \
--source=fluxcdapp \
--path="./deploy/" \
--prune=true \
--validation=client \
--interval=30s \
--export > ./deploy/flux_sync2.yaml