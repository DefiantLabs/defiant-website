---
title: "Sycamore Tax"
date: 2022-12-18T10:30:55-05:00
description: "Cosmos Tax."
page_header_bg : "images/bg/section-bg5.jpg"
image: "images/portfolio/sycamore.png"
author: "Dan Bryan"
draft: true
comments: true
categories: 
  - "Cosmos"
tags:
  - "DeFi"
  - "Taxes"
---


>Sycamore is a Tax App for IBC/Cosmos. It will search all your interchain acitivity and give you reports that can be uploaded to tax software like accointing and koinly.<br><br> 

## Sycamore vs cosmos-tax-cli
The cosmos-tax-cli is an opensource cosmos tax tool that can be used to index any cosmos chain into a postgresql database.  In addition to indexing a chain, it can also search an indexed database for user activity and generate custom CSV reports that can be used with tax software.  Maintaining full archive nodes, postgres database, and understanding how to run CLI tools is both expensive and technically demanding.  This is why we built Sycamore. With Sycamore, you don't need to find or run archive nodes, nor maintain your own databases.  All you do is connect your wallet to sycamore, and we do the rest.  We search all of our databases for chain activity aon your address nd give you a custom report.

## Was Sycamore funded by the community
Sycamore was not funded by the community.  However, the cosmos-tax-cli was funded by the ICF (Interchain Foundation).  We started development on it on February 2022, and contintue to actively develop it.  We have recieved one round of funding for the development work we did between feb-june 2022. This work has been captured in release [v1.0.0](https://github.com/DefiantLabs/cosmos-tax-cli/releases/tag/v1.0.0). We did not directly bill the ICF, but instead worked through Strangelove Ventures as an intermediary.  Strangelove, maintains a fork of the cosmos-tax-cli [here](https://github.com/strangelove-ventures/cosmos-tax-cli). In addition to the ICF funding, we also recieved a grant from the Osmosis Grant Foundation, to add GAMM support to the cosmos-tax-cli.  By Default the cosmos-tax-cli only supports the base cosmos modules identified in the statement of work. By adding support for the GAMM module, it allows users to track LP Activity on osmosis dex, to include joining / leaving pools, and LP rewards.  

## Supported Chains
As mentioned before, the cosmos-tax-cli can index any cosmos chain.  But currently Sycamore only supports Osmosis. We are in the process of adding Cosmoshub, Kujira, and Juno for 2022 tax year. Next year we hope to have 40+ chains fully indexed. If you have a full archive node, and would like to partner with Sycamore, please reach out.

[docs](https://docs.defiantlabs.net/products/sycamore/)  
[app](http://app.sycamore.tax/)

