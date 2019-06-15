---
layout: post
title:  "Crawling an institutional repository with Scrapy"
date:   2019-06-14 15:03:10 -0300
excerpt: How to program a bot to extract data from a university institutional repository.
tags: scrapy scraping crawling data-science brazil science
---

Brazilian society has been discussing whether what we produce in public universities is useful or not. That's a long debate (some context can be found [here](https://g1.globo.com/educacao/noticia/2019/05/15/entenda-o-corte-de-verba-das-universidades-federais-e-saiba-como-sao-os-orcamentos-das-10-maiores.ghtml) and [here](https://www.brasildefato.com.br/2019/05/14/confusao-em-dados-sobre-corte-nas-universidades-federais-e-proposital-diz-professor/)). I've been working on a public university for some time and I have a solid understanding of the benefits that science brings to society. But what exactly do we output? In which subjects do we excel? Do the research projects conducted at my alma mater, the [Universidade Federal do Ceará](http://www.ufc.br) (UFC), for example, match our local potential and needs? Data can help us to answer these questions.

UFC provides [some reports](http://www.ufc.br/a-universidade/ufc-em-numeros), but they do not reveal much about what exactly we have been researching, publishing and developing. Since I couldn't find this information anywhere, I realized that I had to find the answers myself. 

The best place to find out about what a university produces is its institutional repository. Theses, dissertations, articles, reports, all kinds of intellectual output can be found therein. Fortunately, UFC has a [decent repository](http://www.repositorio.ufc.br/) with documents from, at least, some decades ago. This should be enough to provide the information we are interested in.

## Repository structure

The documents in the repository are organized in ["Communities and collections"](http://www.repositorio.ufc.br/community-list). Each community refers to an academic unit, such as "Centro de Ciências" (Sciences Center) or "Instituto de Cultura e Arte" (Institute of Culture and Arts). Each community is formed by its own document collections (which may include theses, dissertations, articles, books, among others) and any associated sub-communities, such as graduate courses and departments. The repository structure is summarized below:

* UFC institutional repository
	* Communities
		* Collections
		* Sub-communities
			* Collections

As an example, let's consider the "Faculdade de Educação" (Education College) community.

* Faculdade de Educação (FACED) 
	* Sub-communities:
		* Departamento de Estudos Especializados;
		* Departamento de Fundamentos da Educação;
		* Departamento de Teoria e Prática do Ensino;
		* Programa de Pós-Graduação em Educação Brasileira.

Each document page contains the following fields:

* Title;
* Authors;
* Advisors;
* Keywords;
* Document date (when it was published or defended?);
* Citation reference;
* Summary (in Portuguese);
* Abstract;
* URI;
* Associated collection;
* Pdf link.

If we collect the data from these fields in *every* document in the repository, we may extract information that would help us to answer our questions. To achieve that, let's consider a scraping tool.

## Scraping the repository

[Scrapy](https://scrapy.org/) is an awesome Python tool to perform automatized scraping and crawling tasks. I wrote a Scrapy script to crawl the whole repository and output the obtained data into a JSON file. The scripts can be found on my Github repository [``import_ufc_repository``](https://github.com/lnribeiro/import_ufc_repository). To run them, you need to have Python and Scrapy installed. You can find the installation guide [here](https://docs.scrapy.org/en/latest/intro/install.html).

Once the environment is set, the ``batch_import.sh`` script may be run to import all communities into JSON files. The script will crawl each repository, looking for documents and following the pagination links.

## Being polite

We have to teach our bots to be polite. Making thousands of requests per second may be overwhelming to the repository server. If they don't behave, we might receive 503 and timeout errors as a response.

One way to teach good manners to our bots is setting the number of concurrent requests and the download delay to one. This can be achieved by setting the following parameters in ``settings.py``:

```
CONCURRENT_REQUESTS = 1
DOWNLOAD_DELAY = 1
```

## The scraped data

On May 17th, 2019, I've run the scripts and got 157,3 MB of scraped data. It can be downloaded [here](https://www.dropbox.com/s/eqa2xkqg2cizo0m/%5Bfull%5D%20scraped%20ufc%20repo%2017%20may.zip?dl=0).

I expect to share with you the insights extracted from these data in the near future.