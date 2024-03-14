<p align="center">
<img src="https://github.com/tomie-s/azure-dns/assets/59409588/08bfed11-3734-4893-8e4e-895c346e5a98" height="45%" width="45%" alt="DNS mockup"/>
</p>


<h1>Understanding DNS, Records Types and Cache</h1>
In this tutorial, we observe a few common DNS record types and DNS cache stored on local computer. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- A-record and CNAME DNS record types


<h2>Operating Systems Used</h2>

- Windows 10 (21H2) (Virtual Machine name: Client-1)
- Windows Server 2022 (Virtual Machine name: DC-1)


<h2>High-Level Steps</h2>

<ul>
  <li>A-Record Exercise</li>
  <li>Local DNS Cache Exercise</li>
  <li>CNAME Record Exercise</li>
</ul>

<h2>Actions and Observations</h2>

<b>A-Record Exercise</b>
<ol>
  <li>Connect/log into Client VM (Client-1) as an admin (ex: newdomain\jane_admin)</li>
  <li>Connect/log into Domain Controller VM (DC-1) as an admin (ex: newdomain\jane_admin) and launch Server Manager</li>
  <li>Using Server Manager Tools, create a DNS A-record for a sub-domain (ex: main.newdomain.com) on DC-1
    <ul>
      <li>have the A-record point back to DC-1’s Private IP address</li>
    </ul>
  </li>
  <li>Go back to Client-1 VM and try to ping the new subdomain created to observe that it works</li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/edae4140-9e26-4e6b-b399-9a394a019c8d" height="70%" width="70%" alt="A-record for subdomain"/>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/a4bbaecc-9bc4-4cfe-b68c-36f5f3599e59" height="70%" width="70%" alt="Successful pin to new subdomain"/>
</p>
<br />


<b>Local DNS Cache Exercise</b>
<ol>
  <li>Go back to DC-1 and change the record address for "main" to 8.8.8.8</li>
  <li>Go back to Client-1 and ping “main” again and observe that it still pings the old address</li>
  <li>Observe the local dns cache (ipconfig /displaydns)</li>
  <li>Flush the DNS cache (ipconfig /flushdns) and observe that the cache is empty</li>
  <li>Attempt to ping “main” again and observe the address of the new record is showing up</li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/50480b49-5791-4f15-b86e-c59a5f3dfea4" height="70%" width="70%" alt="Change A-record IP address"/>
<p>Before and After flushing DNS cache</p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/c7d719bb-3056-4578-a1d0-cf8c42b6f56a" height="45%" width="45%" alt="Ping response before flushing DNS cache"/>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/c7a5d36e-bf8b-4a91-afe7-9ab3facde94f" height="45%" width="45%" alt="Ping response after flushing DNS cache"/>
</p>
<br />



<b>CNAME Record Exercise</b>
<ol>
  <li>In Client-1 VM, attempt to ping “film” to observe the results</li>
  <li>In DC-1 VM, create a CNAME record that points the host “film” to “www.disney.com”</li>
  <li>In Client-1 VM, attempt to ping “film” to observe the results of the CNAME record</li>
  <li>On Client-1, nslookup “search” and observe the results of the CNAME record</li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/b6509034-7408-4260-ad7a-4a9b9551319a" height="70%" width="70%" alt="Create CNAME record"/>
<p>Before and After creating CNAME record</p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/36b40632-1c02-4fd2-aea6-c8b65fd9caef" height="45%" width="45%" alt="Ping response before CNAME record created"/>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/45535b03-37fc-4390-bee8-0804331d73c9" height="45%" width="45%" alt="Ping response after CNAME record created"/>
</p>
<br />


