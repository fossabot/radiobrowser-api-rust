# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.7.22] 2021-11-10
### Fixed
* CHECK: check for http result code for favicons
* PULL: insert duplicates

## [0.7.21] 2021-11-09
### Added
* CHECK: check websites for favicons, if favicon is currently empty
* CLEANUP: recheck favicon every day if still existing and delete from station if not
* CONFIG: regular automatic load/download of config
* CONFIG: reload main config on HUP and regular automatic config reload (does not get used for db connection and api, but for regular jobs)
* CONFIG: added error log level, now there are 5 log levels, 0-4
* CHECK: tags replace
* API: added identifier and image tags to xspf output

### Changed
* CLEANUP: add station change entries into the database for language and favicon updates
* DB: use transactions for migrations
* DB: allow update of existing stations with pulled changes

### Fixed
* CONFIG: replace config in shared memory

## [0.7.20] 2021-10-16
### Added
* CLEANUP: language replace, language to code
* API: iso 639 code output to language list
* DB: use binary collation for tags to fix compare
* CONFIG: allow pulling of replacement csv info from web
* CONFIG: reload csv list files on HUP signal

## [0.7.19] 2021-10-11
### Changed
* DOCKER: use alpine as base image

### Fixed
* CHECK: update stations with new languagecodes
* DB: check for empty lists in streaming servers api
* DB: collect streaming servers only if enabled

## [0.7.18] 2021-10-10
### Changed
* DB: removed fragment and query from streaming server urls
* CHECK: removed fragment and query from streaming server urls
* CLEANUP: remove unreferenced streaming server after 1 day

## [0.7.17] 2021-10-10
### Added
* API: new order type "changetimestamp"
* API: streaming servers
* DB: streaming servers
* CHECK: streaming servers

## [0.7.16] 2021-09-29
### Fixed
* DB: save geolat and geolong to checks table

## [0.7.15] 2021-09-05
### Added
* API: search by extended info marker
* API: search by is_https
* API: exposed iso_3166_2 in station lists

### Fixed
* DB: countrysubdivisioncode is now able to hold full 6 chars

### Updated
* dependencies

## [0.7.14] 2021-05-31
### Fixed
* CHECK: new av-stream-info version does fix handling of depth limit for playlists

## [0.7.13] 2021-05-02
### Added
* API: limit and offset parameters to countries, countrycodes, languages, tags, states, codecs endpoints
* PULL: automatically remove duplicates from database

## [0.7.12] 2021-04-22
### Added
* API: multiple station endpoints do not support limit,offset and hidebroken parameters
* DOCS: added missing hidebroken to advanced search

### Fixed
* API: accept numbers in json post

### Removed
* API: /stations/improvable

## [0.7.11] 2021-04-16
### Fixed
* CHECK: insert of station checks did not always use pregenerated uuids

## [0.7.10] 2021-04-16
### Added
* API: fields server_location and server_country_code to /json/config and /xml/config
* CHECK: added attribute ssl_error to /json/checks endpoint
* API: /json/checksteps, /xml/checksteps, /csv/checksteps
* API: languagecodes, geo_lat, geo_long
* CHECK: extract languagecodes, geo_lat, geo_long
* API: iso 8601 datetime fields

### Changed
* CHECK: do not ignore streams with broken ssl, just mark them
* Dependency upgrade: av-stream-info-rust 0.10.0

### Fixed
* CHECK: do not throw away important check

## [0.7.9] 2021-04-07
### Fixed
* PULL: fixed importing external extra check info

## [0.7.8] 2021-04-07
### Added
* DB: save more information from checks (ServerSoftware, Sampling, LanguageCodes, TimingMs, CountrySubdivisionCode)
* API: add more information for checks

## [0.7.7] 2021-04-05
### Added
* CLEAN: clean urls in db
### Changed
* API: check url and homepage on insert if correct
* CHECK: always ignore text/html urls

## [0.7.6] 2021-04-03
### Added
* API: limit parameter for format/station/changed
* API: limit parameter for format/checks 
* PULL: parameter chunk-size-changes
* PULL: parameter chunk-size-checks

### Fixed
* DB: database name is now allowed to be different from "radio"
* CHECK: bitrate detection of stream works now on multiple bitrate headers
* PULL: try to import stations that are not existing locally for pulled checks
* PULL: votes syncing (#111)

### Changed
* Dependency upgrade: prometheus 0.12.0
* Dependency upgrade: redis 0.20.0
* Dependency upgrade: reqwest 0.11.2
* Dependency upgrade: av-stream-info-rust 0.8.2

## [0.7.5] 2021-01-05
### Changed
* Use do-not-index header of streams to delete them from the database
* Override "Url" field in database if stream override is set
* Support additional stream headers from https://www.stream-meta.info/version_2_headers.html

### Fixed
* DOCKER: added root certificates to container

## [0.7.4] 2020-12-11
### Changed
- PKG: removed mysql dependency from deb package, this enables use of mariadb
### Fixed
* Docker build

## [0.7.3] 2020-12-08
### Added
- API: CSV output

### Changed
- API: ignore country parameter on station add. it is autogenerated from countrycode (ISO 3166-1 Alpha2).
- API: allow only countrycodes with the exact length of 2 on insert.
- API: ignore case on subtable selects (/format/codecs, /format/countries, /format/countrycodes)
- CLEAN: calculate country column in database from countrycode every cleanup cycle
- CLEAN: remove stations from history, that do not have an active entry in main station table

## [0.7.2] 2020-09-14
### Fixed
- API: clicks are counted correctly

## [0.7.1] 2020-06-17
### Added
- API: endpoint for fetching multiple streams by uuid
- PULL: use correct user agent

### Fixed
- CACHE: shorter keys to make memcached work

## [0.7.0] 2020-06-15
### Added
- API: Response caching with builtin, redis and memcached

### Changed
- LOG: Ignore content-type nothing in requests

## [0.6.16] 2020-05-27
### Fixed
- METRICS: do not expose search information in call counts

## [0.6.15] 2020-05-27
### Added
- Support for JSON log format
- Show api call timing information in log file
- Split up api calls in prometheus endpoint with tags

### Fixed
- CLI: Verbose did not work
- Fixed station voting from IPv6 address (Fixed: #69)

### Changed
- DEPENDENCY: Use fern logger instead of env_logger
- API: Use limit parameter if limit is not otherwise provided (Fixed: #64)

### Removed
- API: Old style click count from metrics

## [0.6.14] 2020-04-13
### Fixed
- PLS files had title and file content reversed

## [0.6.13] 2020-04-13
### Fixed
- Always add CORS header, even on errors

### Added
- Answer OPTIONS requests for better support of CORS

## [0.6.12] 2020-04-12
### Added
- METRICS: station_clicks, api_calls
- API: codec parameter to advanced search

### Fixed
- Use utc timestamp for clicks in database

## [0.6.11] 2020-02-17
### Added
- API: Added stationuuid to m3u output

### Fixed
- API: Filter order column for extra tables

## [0.6.10] 2020-02-01
### Fixed
- API: Wrong links in docs
- API: Faster select from stationcheck view with added index
- SYNC: Only update stations with changed votes
- SYNC: Faster update of station's clicks with added index

## [0.6.9] 2020-02-01
### Added
- DEB: logrotate config
- API: more exports to metrics
- API: config endpoint

### Fixed
- API: return change lists (stations, checks, clicks) from start if lastuuid not found

### Changed
- CLEANUP: remove all non http/https content from favicon field of stations
- ANSIBLE: disabled all apache2 logging by default
- CONFIG: type errors do not get ignored with default value
- CONFIG: use human readable durations instead of fixed seconds or hours

## [0.6.8] 2020-01-22
### Fixed
- Fixed wrong sql delete
- Ignore station checks and clicks on pull, when there is no station

### Added
- Show "hidebroken" in docs for station query

## [0.6.7] 2020-01-19
### Fixed
- Migrations on mysql

## [0.6.6] 2020-01-19
### Added
- Simple sync of votes, may drop some votes

### Fixed
- Broken stations were not marked
- Make foreign keys of StationClick and StationCheckHistory on delete cascade

## [0.6.5] 2020-01-18
### Added
- Ansible role and example playbook for debian/ubuntu

### Fixed
- Station checks
- Always use UTC time in database
- Faster check insert with mysql 5.7

### Changed
- Default install paths changed
- IPs for clicks are only kept until not needed anymore (default 24 hours)

## [0.6.4] 2020-01-14
### Fixed
- Insert of checks does now ignore duplicates
- Resuse checkuuids of pullserver, do not generate new ones on pull
- Incremental results of /format/stations/changed, /format/checks and /format/clicks do work reliably

### Changed
- Replaced StationCheck table with view on StationCheckHistory
- Migration deletes contents of StationCheckHistory, to remove unconnected uuids
- Migration deletes contents of PullServers to force re-pulling of every server

## [0.6.3] 2020-01-12
### Added
- Script for building distribution file

### Changed
- Debian package
- Improved readme

## [0.6.2] 2020-01-11
### Added
- Sync for clicks
- Api for clicks /format/clicks

### Changed
- Document "/format/url" endpoint as station click endpoint
- Document returned structs "station", "checks"
- Faster sync

### Fixed
- Clickcount calculation for each station
- Error in /format/stations/changed endpoint

## [0.6.1] 2020-01-08
### Added
- Prometheus docs

### Fixed
- SQL error in endpoint /checks?seconds=x
- Database column mixup for state and language

### Changed
- Run as non root user in docker by default

## [0.6.0] - 2020-01-06
### Added
- Changelog
- Check fields: "metainfo_overrides_database", "public", "name", "description", "tags", "countrycode", "homepage", "favicon", "loadbalancer"

### Removed
- "id" from all of the API, because database id should not be exposed
- Endpoint /stations/broken 

### Changed
- Faster station import from pull source
- Restructured more code to the new style of connecting to the database, this should enable other types of databases (e.g.: postgresql) on the long term, this means also more error checking and use of transactions.

### Fixed
- Output lastchangetime and countrycode in /json/stations/changed
- Correctly collect and summarize different sources of station checks
- "numberofentries" added to pls output
- Less usages of "unwrap()"

## [0.5.1] - 2019-12-11
### Added
- "url_resolved" field to station lists
- "random" order to station lists

### Removed
- "negativevotes" field from station lists

### Fixed
- Fixed json result of vote endpoint
- Clean up tag and language fields on import
- Documentation cleanup and extensions

## [0.5.0] - 2019-12-08
### Added
- First documented release :)
