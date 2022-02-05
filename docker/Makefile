.DEFAULT_GOAL := help

.PHONY: help

CONTAINER_ENGINE = docker

OS_IMAGE_VERSION = 20.04
OS_IMAGE         = docker.io/library/ubuntu
OS_TAG           = $(OS_IMAGE):$(OS_IMAGE_VERSION)

REBOUND_VERSION = latest
REBOUND_IMAGE   = rebound
REBOUND_TAG     = $(REBOUND_IMAGE):$(REBOUND_VERSION)

PYTHON_EXAMPLE_DIR  = ./python_examples/
PYTHON_EXAMPLE      = simple_orbit/problem.py

pull-os: ## pull operating system
	@$(CONTAINER_ENGINE) pull $(OS_TAG)

rebound-tag: pull-os ## tag rebound image
	@$(CONTAINER_ENGINE) tag $(OS_TAG) $(REBOUND_TAG)

rebound-build: rebound-tag
	@cd ./docker && $(CONTAINER_ENGINE) build -t $(REBOUND_TAG) .

rebound-up: rebound-build
	@cd ./docker && $(CONTAINER_ENGINE)-compose up -d $(REBOUND_IMAGE)

rebound-python-example: rebound-up ## run a python_examples/simple_orbit/problem.py
	$(CONTAINER_ENGINE) exec -it $(REBOUND_IMAGE) bash -c "python3 $(PYTHON_EXAMPLE_DIR)/$(PYTHON_EXAMPLE)" 

help: ## That's me!
	@printf "\033[37m%-30s\033[0m %s\n" "#----------------------------------------------------------------------------------"
	@printf "\033[37m%-30s\033[0m %s\n" "# Makefile targets                          |"
	@printf "\033[37m%-30s\033[0m %s\n" "#----------------------------------------------------------------------------------"
	@printf "\033[37m%-30s\033[0m %s\n" "#-target-----------------------description-----------------------------------------"
	@grep -E '^[a-zA-Z0-9].+:.*?## .*$$' Makefile | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

print-%:
	@echo $* = $($*)