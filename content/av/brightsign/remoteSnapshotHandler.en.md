---
title: BrightSign remoteSnapshotHandler.php sample
date: 2020-03-12
description: Simple PHP Script to accept snapshots from BrightSign players
tags: brightsign, php
---

# Problem
BrightSign players (https://www.brightsign.biz) allow remote uploads of snapshots to external webservers.

Because the "near future" did not arrived since 2015 (https://brightsign.zendesk.com/hc/en-us/community/posts/209964857-remote-snapshot-for-SFN) i wrote a simple PHP script to accept these snapshots.


# Howto
Create a file and configure your webserver to get it executed with a url.

This sample script assumes  
`your_webroot/brightsign-snapshot/index.php`  
which get mapped to  
`https://your-domain.com/brightsign-snapshot/`  
as example.

You could also just create a `remoteSnapshotHandler.php` and call it with it's name.

To identify a player, you have to append a system name to the URL:

`https://your-domain.com/brightsign-snapshot/?system=garage`


The simple script:
```php
<?php
// Request looks like this: "PUT /brightsign-snapshot/?system=my_brightsign_id HTTP/1.1" 200 - "-" "BrightSign/8.0.127 (LS424)"

if (!isset($_REQUEST["system"])) {
  // "system" parameter is mandatory.
  die("Wrong identifier");  
}
 
if ($_SERVER['REQUEST_METHOD'] != "PUT") {
  // PUT requests only
  die("Bad request method.");
}

// Get identifier
$system = $_REQUEST["system"];

// Open data stream for read
$putdata = fopen("php://input","r");

// Create current time
$now = new DateTime("NOW"); 
$now_str = $now->format('Y-m-d_H-i-s');

// Open data stream to write
// Make sure the script has write access to your specified folder!
$fp = fopen("/tmp/".$system."_".$now_str.".jpg", "w");
// "/tmp" may be mapped to an isolated directory caused by systemd.
// in my case it's in `/tmp/systemd-private-8e6ed5800c4044b4ae5e637b67c41b39-httpd.service-HiCJGf/tmp`

while ($data = fread($putdata,1024))
  fwrite($fp,$data);

// Close streams
fclose($fp);
fclose($putdata);
?>
```

Files will be saved like this:  
`garage_2020-03-12_14-03-28.jpg`
