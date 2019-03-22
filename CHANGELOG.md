# Changelog

This file contains all notable changes to
[imageproxy](https://github.com/willnorris/imageproxy).  The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
[Unreleased]: https://github.com/willnorris/imageproxy/compare/v0.8.0...HEAD

### Changed
 - updated docker image to use go1.12 compiler and build imageproxy as a go module.

### Removed
 - removed deprecated `whitelist` flag and `Proxy.Whitelist` struct field. Use
   `allowHosts` and `Proxy.AllowHosts` instead.

## [0.8.0] (2019-03-21)
[0.8.0]: https://github.com/willnorris/imageproxy/compare/v0.7.0...v0.8.0

### Added
 - added support for restricting proxied URLs [based on Content-Type
   headers](https://github.com/willnorris/imageproxy#allowed-content-type-list)
   ([#141](https://github.com/willnorris/imageproxy/pull/141),
   [ccbrown](https://github.com/ccbrown))
 - added ability to [deny requests](https://github.com/willnorris/imageproxy#allowed-and-denied-hosts-list)
   for certain remote hosts
   ([#85](https://github.com/willnorris/imageproxy/pull/85),
   [geriljaSA](https://github.com/geriljaSA))
 - added `userAgent` flag to specify a custom user agent when fetching images
   ([#83](https://github.com/willnorris/imageproxy/pull/83),
   [huguesalary](https://github.com/huguesalary))
 - added support for [s3 compatible](https://github.com/willnorris/imageproxy#cache)
   storage providers
   ([#147](https://github.com/willnorris/imageproxy/pull/147),
   [ruledio](https://github.com/ruledio))
 - log URL when image transform fails for easier debugging
   ([#149](https://github.com/willnorris/imageproxy/pull/149),
   [daohoangson](https://github.com/daohoangson))
 - added support for building imageproxy as a [go module](https://golang.org/wiki/Modules).
   A future version will remove vendored dependencies, at which point building
   as a module will be the only supported method of building imageproxy.

### Changed
 - when a remote URL is denied, return a generic error message that does not specify exactly why it failed
   ([7e19b5c](https://github.com/willnorris/imageproxy/commit/7e19b5c))

### Deprecated
 - `whitelist` flag and `Proxy.Whitelist` struct field renamed to `allowHosts`
   and `Proxy.AllowHosts`.  Old values are still supported, but will be removed
   in a future release.

### Fixed
 - fixed tcp_mem resource leak on 304 responses
   ([#153](https://github.com/willnorris/imageproxy/pull/153),
   [Micr0mega](https://github.com/Micr0mega))

## [0.7.0] (2018-02-06)
[0.7.0]: https://github.com/willnorris/imageproxy/compare/v0.6.0...v0.7.0

### Added
 - added support for arbitrary [rectangular crops](https://godoc.org/willnorris.com/go/imageproxy#hdr-Rectangle_Crop)
   ([#90](https://github.com/willnorris/imageproxy/pull/90),
   [maciejtarnowski](https://github.com/maciejtarnowski))
 - added support for tiff images
   ([#109](https://github.com/willnorris/imageproxy/pull/109),
   [mikecx](https://github.com/mikecx))
 - added support for additional [caching backends](https://github.com/willnorris/imageproxy#cache):
    - Google Cloud Storage
      ([#106](https://github.com/willnorris/imageproxy/pull/106),
      [diegomarangoni](https://github.com/diegomarangoni))
    - Azure
      ([#79](https://github.com/willnorris/imageproxy/pull/79),
      [PaulARoy](https://github.com/PaulARoy))
    - Redis
      ([#49](https://github.com/willnorris/imageproxy/issues/49)
      [dbfc693](https://github.com/willnorris/imageproxy/commit/dbfc693))
    - Tiering multiple caches by repeating the `-cache` flag
      ([ec5b543](https://github.com/willnorris/imageproxy/commit/ec5b543))
 - added support for EXIF orientation tags
   ([#63](https://github.com/willnorris/imageproxy/issues/63),
   [67619a6](https://github.com/willnorris/imageproxy/commit/67619a6))
 - added [smart crop feature](https://godoc.org/willnorris.com/go/imageproxy#hdr-Smart_Crop)
   ([#55](https://github.com/willnorris/imageproxy/issues/55),
   [afbd254](https://github.com/willnorris/imageproxy/commit/afbd254))

### Changed
 - rotate values are normalized, such that `r-90` is the same as `r270`
   ([07c54b4](https://github.com/willnorris/imageproxy/commit/07c54b4))
 - now return `200 OK` response for requests to root `/`
   ([5ee7e28](https://github.com/willnorris/imageproxy/commit/5ee7e28))
 - switch to using official AWS Go SDK for s3 cache storage.  This is a
   breaking change for anyone using that cache implementation, since the URL
   syntax has changed.  This adds support for the newer v4 auth method, as well
   as additional s3 regions.
   ([0ee5167](https://github.com/willnorris/imageproxy/commit/0ee5167))
 - switched to standard go log library.  Added `-verbose` flag for more logging
   in-memory cache backend supports limiting the max cache size
   ([a57047f](https://github.com/willnorris/imageproxy/commit/a57047f))
 - docker image sized reduced by using scratch image and multistage build
   ([#113](https://github.com/willnorris/imageproxy/pull/113),
   [matematik7](https://github.com/matematik7))

### Removed
 - removed deprecated `cacheDir` and `cacheSize` flags

### Fixed
 - fixed interpretation of `Last-Modified` and `If-Modified-Since` headers
   ([#108](https://github.com/willnorris/imageproxy/pull/108),
   [jamesreggio](https://github.com/jamesreggio))
 - preserve original URL encoding
   ([#115](https://github.com/willnorris/imageproxy/issues/115))

## [0.6.0] (2017-08-29)
[0.6.0]: https://github.com/willnorris/imageproxy/compare/v0.5.1...v0.6.0

## [0.5.1] (2015-12-07)
[0.5.1]: https://github.com/willnorris/imageproxy/compare/v0.5.0...v0.5.1

## [0.5.0] (2015-12-07)
[0.5.0]: https://github.com/willnorris/imageproxy/compare/v0.4.0...v0.5.0

## [0.4.0] (2015-05-21)
[0.4.0]: https://github.com/willnorris/imageproxy/compare/v0.3.0...v0.4.0

## [0.3.0] (2015-12-07)
[0.3.0]: https://github.com/willnorris/imageproxy/compare/v0.2.3...v0.3.0

## [0.2.3] (2015-02-20)
[0.2.3]: https://github.com/willnorris/imageproxy/compare/v0.2.2...v0.2.3

## [0.2.2] (2014-12-08)
[0.2.2]: https://github.com/willnorris/imageproxy/compare/v0.2.1...v0.2.2

## [0.2.1] (2014-08-13)
[0.2.1]: https://github.com/willnorris/imageproxy/compare/v0.2.0...v0.2.1

## [0.2.0] (2014-07-02)
[0.2.0]: https://github.com/willnorris/imageproxy/compare/v0.1.0...v0.2.0

## [0.1.0] (2013-12-26)
[0.1.0]: https://github.com/willnorris/imageproxy/compare/5d75e8a...v0.1.0
