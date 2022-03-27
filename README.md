[hex-img]: http://img.shields.io/hexpm/v/waffle.svg
[hex-url]: https://hex.pm/packages/waffle

[hexdocs-img]: http://img.shields.io/badge/hexdocs-documentation-brightgreen.svg
[hexdocs-url]: https://hexdocs.pm/waffle

[evrone-img]: https://img.shields.io/badge/Sponsored_by-Evrone-brightgreen.svg
[evrome-url]: https://evrone.com?utm_source=waffle

# Waffle [![Sponsored by Evrone][evrone-img]][evrome-url]

[![Hex.pm Version][hex-img]][hex-url]
[![waffle documentation][hexdocs-img]][hexdocs-url]

<img align="right" width="176" height="120"
     alt="Waffle is a flexible file upload library for Elixir"
     src="https://elixir-waffle.github.io/waffle/assets/logo.svg">

Waffle is a flexible file upload library for Elixir with straightforward integrations for Amazon S3 and ImageMagick.

[Documentation](https://hexdocs.pm/waffle)

## Installation

Add the latest stable release to your `mix.exs` file, along with the
required dependencies for `ExAws` if appropriate:

```elixir
defp deps do
  [
    {:waffle, "~> 1.1"},

    # If using S3:
    {:ex_aws, "~> 2.1.2"},
    {:ex_aws_s3, "~> 2.0"},
    {:hackney, "~> 1.9"},
    {:sweet_xml, "~> 0.6"}
  ]
end
```

Then run `mix deps.get` in your shell to fetch the dependencies.

## Usage

After installing Waffle, another two things should be done:

1. setup a storage provider
2. define a definition module

### Setup a storage provider

Waffle has two built-in storage providers:

* `Waffle.Storage.Local`
* `Waffle.Storage.S3`

[Other available storage providers](#other-storage-providers)
are supported by the community.

An example for setting up `Waffle.Storage.Local`:

```elixir
config :waffle,
  storage: Waffle.Storage.Local,
  asset_host: "http://static.example.com" # or {:system, "ASSET_HOST"}
```

An example for setting up `Waffle.Storage.S3`:

```elixir
config :waffle,
  storage: Waffle.Storage.S3,
  bucket: "custom_bucket",                # or {:system, "AWS_S3_BUCKET"}
  asset_host: "http://static.example.com" # or {:system, "ASSET_HOST"}

config :ex_aws,
  json_codec: Jason
  # any configurations provided by https://github.com/ex-aws/ex_aws
```

### Define a definition module

Waffle requires a **definition module** which contains the relevant
functions to store and retrieve files:

* Optional transformations of the uploaded file
* Where to put your files (the storage directory)
* How to name your files
* How to secure your files (private? Or publicly accessible?)
* Default placeholders

This module can be created manually or generated by `mix waffle.g`
automatically.

As an example, we will generate a definition module for handling
avatars:

    mix waffle.g avatar

This should generate a file at `lib/[APP_NAME]_web/uploaders/avatar.ex`.
Check this file for descriptions of configurable options.

## Examples

* [An example for Local storage driver](documentation/examples/local.md)
* [An example for S3 storage driver](documentation/examples/s3.md)

## Usage with Ecto

Waffle comes with a companion package for use with Ecto. If you
intend to use Waffle with Ecto, it is highly recommended you also
add the
[`waffle_ecto`](https://github.com/elixir-waffle/waffle_ecto)
dependency.  Benefits include:

  * Changeset integration
  * Versioned urls for cache busting (`.../thumb.png?v=63601457477`)

## Other Storage Providers

  * **Rackspace** - [arc_rackspace](https://github.com/lokalebasen/arc_rackspace)

  * **Manta** - [arc_manta](https://github.com/onyxrev/arc_manta)

  * **OVH** - [arc_ovh](https://github.com/stephenmoloney/arc_ovh)

  * **Google Cloud Storage** - [waffle_gcs](https://github.com/kolorahl/waffle_gcs)

  * **Microsoft Azure Storage** - [arc_azure](https://github.com/phil-a/arc_azure)

  * **Aliyun OSS Storage** - [waffle_aliyun_oss](https://github.com/ug0/waffle_aliyun_oss)

## Attribution

Great thanks to Sean Stavropoulos (@stavro) for the original awesome work on the library.

This project is forked from [Arc](https://github.com/stavro/arc) from the version `v0.11.0`.

## License

Copyright 2019 Boris Kuznetsov <me@achempion.com>

Copyright 2015 Sean Stavropoulos

  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
