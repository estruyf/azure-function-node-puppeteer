# Azure Functions Docker image with support for Puppeteer

[![Pulls from Docker Hub](https://img.shields.io/docker/pulls/estruyf/azure-function-node-puppeteer.svg)](https://hub.docker.com/r/estruyf/azure-function-node-puppeteer)
[![Stars on Docker Hub](https://img.shields.io/docker/stars/estruyf/azure-function-node-puppeteer.svg)](https://hub.docker.com/r/estruyf/azure-function-node-puppeteer)

## Why use this image?

You probably want to use Puppeteer in your Azure Function. This Docker image got you covered.

## Usage

Initialize a new project for your Azure Functions:

```
func init --docker
```

Update the Dockerfile with the following contents:

```
FROM estruyf/azure-function-node-puppeteer

COPY . /home/site/wwwroot
```

## Using Puppeteer

Once you create a new Azure Function, you can use it like this sample:

```
const puppeteer = require('puppeteer');

module.exports = async (context, req) => {    
    const browser = await puppeteer.launch({
        args: [
            '--no-sandbox',
            '--disable-setuid-sandbox'
        ]
    });

    const page = await browser.newPage();
    await page.goto('https://www.eliostruyf.com');
    const pageTitle = await page.title();
    await browser.close();

    context.res = {
        // status: 200, /* Defaults to 200 */
        body: `Page title: ${pageTitle}`
    };
};
```