# CBI Website

This repository contains the source code and configuration for the CBI (Common Build Infrastructure) website, built using [MkDocs-material](https://squidfunk.github.io/mkdocs-material/).

[TOC]

## Getting Started

### Prerequisites

Before setting up the project, ensure you have the following installed:
- **Python 3.7+**
- **pip** (Python package manager)

### Installation

Clone the repository and install the dependencies:

```bash
git clone https://github.com/eclipse-cbi/cbi-website.git
cd cbi-website
pip install -r requirements.txt
```

## Local Development

Run the following command to serve the website locally:

```bash
mkdocs serve
```

Open your browser and navigate to http://127.0.0.1:8000 to view the website.

## Building the site

To build the static files for deployment, run:

```bash
mkdocs build
```

The static files will be generated in the `site/` directory.

## Deploy the site

The CBI Website can be deployed with the following command:

```bash
mkdocs gh-deploy
```

This will push the contents of the `site/` directory to the gh-pages branch.

