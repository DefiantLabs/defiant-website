---
title: "About Us"
page_header_bg: "images/bg/section-bg5.jpg"
description: "This is meta description"
layout: "about"
draft: false

######################### Counter ####################
counter:
  enable: true
  title : "We build tools for the Cosmos Ecosystem."
  counter_item:
  # counter item loop
  - icon : "ti-thumb-up" # here we use themify icon pack : https://themify.me/themify-icons
    title : "Current Projects"
    count : "2"
    unit : "+"
    
  # counter item loop
  - icon : "ti-world" # here we use themify icon pack : https://themify.me/themify-icons
    title : "Our Contirbutions"
    count : "2"
    unit : ""
    
  # counter item loop
  - icon : "ti-cloud" # here we use themify icon pack : https://themify.me/themify-icons
    title : "Platforms"
    count : "3"
    unit : ""

####################### Promo video ######################
video:
  enable: false
  title : "Growing Software Company Since 2008"
  video_thumb: "images/about/img-34.png"
  video_embed_link : "https://www.youtube.com/embed/dyZcRRWiuuw"
  content : "
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sint earum, eos esse non error facilis ad, maiores eum quae vero libero voluptas! Reprehenderit sunt similique, quae quidem voluptatem odit natus.


  * Create and manage any process for your business needs.

  * Create and manage any process for your business needs.

  * Create and manage any process for your business needs.
  "
  button:
    enable : true
    label : "All Services"
    link : "service"

################################## Team ########################
team:
  enable : true
  title : "Our Team"
  content : "Defiant Labs is a growing company made up of talented individuals with different backgrounds."

  team_member:
  # team member loop
  - name : "Dan Bryan"
    image : "images/team/dan.png"
    designation : "Founder"

  - name : "Kyle Moser"
    image : "images/team/kyle.png"
    designation : "Founder"
    

################################ Clients ######################
clients:
  enable : true
  title : "Our Contributions"
  content : ""
  logos:
  - "images/clients/cosmos.png"


################################ Platforms ######################
platforms:
  enable : true
  title : "Supported platforms"
  content : ""
  logos:
  - "images/platforms/aws.png"
  - "images/platforms/google-cloud.png"


########################## Testimonial ########################
testimonial:
  enable: true
  # testimonial content comes from "data/homepage.yml" file.
---