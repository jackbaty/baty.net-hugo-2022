---
title: "Search"
date: 2022-07-29T05:08:20-04:00
draft: false
excludeFromTopNav: false
url: "/search/"
# set the link if you want to redirect the user.
link: ""
weight: 0
---

<link href="/_pagefind/pagefind-ui.css" rel="stylesheet">
<script src="/_pagefind/pagefind-ui.js" type="text/javascript"></script>
<div id="search"></div>
<script>
    window.addEventListener('DOMContentLoaded', (event) => {
        new PagefindUI({ element: "#search" });
    });
</script>