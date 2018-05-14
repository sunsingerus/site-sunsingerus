---
ID: 446
post_title: AWS. Manage Key Pairs
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/aws-manage-key-pairs/
published: true
post_date: 2018-05-14 11:05:20
---
<h1>Create New Key Pair</h1>

Open <code>Services -> EC2</code>
On the left side menu select <code>Key Pairs</code> and then click <code>Create Key Pair</code>
<img src="https://sunsingerus.com/wp-content/uploads/2018/05/1_create_key_pair.png" alt="" width="483" height="183" class="alignnone size-full wp-image-447" />
Let's call it <code>ubuntu_key_pair</code> and click <code>Create</code>
Download <code>.pem</code> file
<img src="https://sunsingerus.com/wp-content/uploads/2018/05/2_download_pem_file.png" alt="" width="500" height="500" class="alignnone size-full wp-image-448" />
which contains <strong>private key</strong>, with the content like the following:
<pre>
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAqgJJItUsUicOuTeW9PoCRxYetS63e5Qh4Ee18Y6lx+zoWT0EIF3HYdJvdZR+
...
bj84nUsk2odCOD3+pGjzGaX13U0o4kCi+Pm0CBf342ICqyvDpnmOkEiH7adS1qxZdZE0
-----END RSA PRIVATE KEY-----
</pre>

<h1>Delete key Pair</h1>
Select Key Pair to be deleted and click <code>Delete Pair</code>
<img src="https://sunsingerus.com/wp-content/uploads/2018/05/3_delete_key_pair.png" alt="" width="467" height="222" class="alignnone size-full wp-image-453" />

<h1>Import Existing Key Pair</h1>
Click <code>Import Key Pair</code> and select file with <strong>public key</strong> of the key pair. <strong>IMPORTANT</strong> - <code>.pem</code> file downloaded in <strong>Create New Key Pair</strong> section earlier will NOT do - it contains <strong>private key</strong>. So you need to generate <strong>public key</strong> out of <strong>private key</strong> in case you have <code>.pem</code> file only. This can be done with the help of multiple tools, and <strong>puttygen</strong> from <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html" rel="noopener" target="_blank">PuTTY</a> is one of my favorite.

So, having <strong>public key</strong> available, let's upload it:
<img src="https://sunsingerus.com/wp-content/uploads/2018/05/4_import_public_key_from_the_pair.png" alt="" width="674" height="410" class="alignnone size-full wp-image-454" />
 and we'll see new key pair available.