#!/usr/bin/env make

# Import de la configuration environnementale
include ../../etc/$(ENVIRONMENT)/.env
export $(shell sed 's/=.*//' ../../etc/$(ENVIRONMENT)/.env)
include .env
export $(shell sed 's/=.*//' .env)

# Commandes publiques

## Misc

help: ## Affichage de ce message d'aide
	@printf "\033[36m%s\033[0m \n\n" $$(basename $$(pwd))
	@echo "Commandes\n"
	@for MKFILE in $(MAKEFILE_LIST); do \
		grep -E '^[a-zA-Z0-9\._-]+:.*?## .*$$' $$MKFILE | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m  %-30s\033[0m  %s\n", $$1, $$2}'; \
	done
	@echo ""
	@echo "Endpoints"
	@echo
	@echo "  \033[36mTraefik\033[0m : http://$${TRAEFIK_FQDN}"

## Contrôle des conteneurs

clean: stop ## Suppresssion des conteneurs
	docker-compose -p $${COMPOSE_PROJECT_NAME}-traefik rm -f

purge: ## Suppression des volumes
	sudo rm -rf ../../var/traefik

start: ## Démarrage du composant
	docker-compose -p $${COMPOSE_PROJECT_NAME}-traefik up --remove-orphans -d

stop: ## Arrêt arrêt du composant
	docker-compose -p $${COMPOSE_PROJECT_NAME}-traefik stop

