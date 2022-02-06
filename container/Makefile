.DEFAULT_GOAL := help

.PHONY: help

CONTAINER_ENGINE = docker

# OS of IMAGE
OS_IMAGE_VERSION = 20.04
OS_DISTRO        = ubuntu
OS_IMAGE         = docker.io/library/$(OS_DISTRO)
OS_TAG           = $(OS_IMAGE):$(OS_IMAGE_VERSION)

REBOUND_VERSION = latest
REBOUND_IMAGE   = rebound
REBOUND_TAG     = $(REBOUND_IMAGE):$(REBOUND_VERSION)

PYTHON_EXAMPLE_DIR  = ./python_examples
PYTHON_EXAMPLE      = simple_orbit

PYTHON_EXAMPLES=$(shell cd $(PYTHON_EXAMPLE_DIR) && find . -type f)

pull-image:
	@echo
	@echo pulling $(OS_TAG) using CONTAINER_ENGINE=$(CONTAINER_ENGINE)
	@echo
	@$(CONTAINER_ENGINE) pull $(OS_TAG)

rebound-tag: pull-image
	@echo
	@echo tagging $(OS_TAG) as $(REBOUND_TAG) using CONTAINER_ENGINE=$(CONTAINER_ENGINE)
	@echo
	@$(CONTAINER_ENGINE) tag $(OS_TAG) $(REBOUND_TAG)

rebound-build: rebound-tag
	@echo
	@echo tagging $(OS_TAG) as $(REBOUND_TAG) using CONTAINER_ENGINE=$(CONTAINER_ENGINE)
	@echo
	cd ./container && $(CONTAINER_ENGINE) build \
		-t $(REBOUND_TAG) . \
		--build-arg OS_TAG=$(OS_TAG)

rebound-down: ## bring down the rebound container
	@cd ./container && $(CONTAINER_ENGINE)-compose down --remove-orphans

rebound-up: rebound-build ## bring up the rebound container
	@cd ./container && $(CONTAINER_ENGINE)-compose up -d

rebound-python-example: rebound-up ## run example ./python_examples/simple_orbit/problem.py
	@time $(CONTAINER_ENGINE) exec -it $(REBOUND_IMAGE) bash -c "python3 $(PYTHON_EXAMPLE_DIR)/$(PYTHON_EXAMPLE)/problem.py" 

# TODO: need to figure out below
# rebound-all-python-examples: rebound-up ## run all python examples found in ./python_examples
# 	$(CONTAINER_ENGINE) exec -it $(REBOUND_IMAGE) bash -c " \
# 	examples=($(PYTHON_EXAMPLES)); \
# 	date; \
# 	for example in $${examples[@]}; \
# 	do \
# 	echo $$example; \
# 	done; \
# 	python3 $(PYTHON_EXAMPLE_DIR)/$(PYTHON_EXAMPLE) \
# 	" 

help: ## That's me!
	@printf "\033[37m%-30s\033[0m %s\n" "#----------------------------------------------------------------------------------"
	@printf "\033[37m%-30s\033[0m %s\n" "# Makefile targets                          |"
	@printf "\033[37m%-30s\033[0m %s\n" "#----------------------------------------------------------------------------------"
	@printf "\033[37m%-30s\033[0m %s\n" "#-target-----------------------description-----------------------------------------"
	@grep -E '^[a-zA-Z0-9].+:.*?## .*$$' Makefile | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

print-%:
	@echo $* = $($*)