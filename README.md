# discourse-elasticsearch

discourse-elasticsearch is a plugin for elasticsearch

## Installation

Follow [Install a Plugin](https://meta.discourse.org/t/install-a-plugin/19157)

Installation
Add this repository's git clone url to your container's app.yml file, at the bottom of the cmd section:

```yml
hooks:
  after_code:
    - exec:
        cd: $home/plugins
        cmd:
          - mkdir -p plugins
          - git clone https://github.com/imMMX/discourse-elasticsearch.git
```
          

Rebuild your container:

```
cd /var/discourse
git pull
./launcher rebuild app
```

## Configuration

Once you've installed the plugin and restarted your Discourse, you will see a new plugin available in your admin configuration. Click the Settings button next to the discourse-elasticsearch plugin.

## Initial indexing

You can now index all of your forum's content. Run the following rake task in your Discourse directory:

```
./launcher enter app
su discourse
LOAD_PLUGINS=1 bundle exec rails algolia:initialize
```
This will create and configure three indices - discourse-users, discourse-posts, and discourse-tags - and then populate them by loading data from your database and sending it to Elasticsearch. 

## Rake tasks

```
rake elasticsearch:configure                                                 # configure elasticsearch index settings
rake elasticsearch:initialize                                                # configure indices and upload data
rake elasticsearch:reindex                                                   # reindex everything to elasticsearch
rake elasticsearch:reindex_posts                                             # reindex posts in elasticsearch
rake elasticsearch:reindex_tags                                              # reindex tags in elasticsearch
rake elasticsearch:reindex_users                                             # reindex users in elasticsearch
```

## Usage

## Feedback

If you have issues or suggestions for the plugin, please open an issue.