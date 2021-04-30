# Cheat Sheet Generator

## Hosted on github pages

Cheat sheets are hosted on github pages : [https://timsayshey.github.io/cfml-cheatsheets/](https://timsayshey.github.io/cfml-cheatsheets/)

## Browsers support <sub><sup><sub><sub>made by </sub></sub></sup></sub>





| last 2 versions

## Install

NodeJS version 6+

gulp is needed in global in order to run compilation :

`npm install gulp -g`

`yarn`
or
`npm install`

## Usage

From install folder:

`gulp create-new-cheat-sheet --name <name> --category <toolsbest-practices>`

Put your svg|png logo in assets/images folder
Put your commands or codes on:

- src/\<name\>/first-side/column1.md
- src/\<name\>/first-side/column2.md
- src/\<name\>/reverse/column1.md
- src/\<name\>/reverse/column2.md

## Devtools

Build and reload server:

`gulp watch`

## Print

- Hit `Ctrl+P` to generate the PDF version, using `Save as PDF`
- Disable margins
