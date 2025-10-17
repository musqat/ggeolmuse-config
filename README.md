# GGeolmuse Configuration Repository

This repository contains configuration files for GGeolmuse microservices.

## Structure

- `{service-name}.yml`: Default configuration for a service
- `{service-name}-{profile}.yml`: Profile-specific configuration

## Services

- gateway-server
- user-service
- trade-service
- market-data-service
- backtest-service

## Profiles

- dev: Development environment
- prod: Production environment

## Usage

Config Server reads from this repository using Git backend.

Application Name: `gateway-server`
Profile: `dev`
→ Loads: `gateway-server.yml` + `gateway-server-dev.yml`
