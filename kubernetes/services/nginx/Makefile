CHART := bitnami/nginx
CHART_VERSION := 25.2.5
RELEASE := nginx
NAMESPACE := nginx

GENERATED_DIR := generated
HELM_MANIFEST := $(GENERATED_DIR)/template.helm.manifest.yaml
FINAL_MANIFEST := $(GENERATED_DIR)/final.manifest.yaml

.PHONY: render build deploy clean

render:
	mkdir -p $(GENERATED_DIR)
	helm template $(RELEASE) $(CHART) \
		--version $(CHART_VERSION) \
		--namespace $(NAMESPACE) \
		-f service-base.values.yaml \
		-f values.yaml \
		> $(HELM_MANIFEST)

build: render
	kubectl kustomize . > $(FINAL_MANIFEST)

deploy: build
	kubectl apply -f $(FINAL_MANIFEST)

clean:
	rm -rf $(GENERATED_DIR)