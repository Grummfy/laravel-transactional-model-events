# Changelog

All notable changes to `laravel-transactional-model-events` will be documented in this file

## 2.1.0 - 2020-01-07

- Removed support for php 7.1
- Added support for php 7.4
- Fixed dependencies so it properly tests against latest laravel version
- Ignore laravel version 6.9.0 which broke this package and is fixed from 6.10.0 [more information](https://github.com/laravel/framework/issues/30948)

## 2.0.0 - 2019-08-28

- Add support for observers
- removed support for laravel 5.5 and 5.6
- Added support for laravel 6.0

## 1.0.1 - 2019-06-13

- fix firing model events with nested transactions. Only when outer transaction is committed the model events are fired.

## 1.0.0 - 2019-05-19

- initial release
