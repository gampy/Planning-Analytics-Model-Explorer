<div style="display: flex; align-items: center;">
  <a href="https://exploredata.pro/planning-analytics-explorer/" style="text-decoration: none; color: inherit;">
   <img src="https://exploredata.pro/wp-content/uploads/pa-model-explorer/pics/pa-model-explorer-logo.png" alt="Planning Analytics Model Explorer">
  </a>
</div>


# Configuring IBM Planning Analytics
1.	Set the following parameters in the tm1s.cfg configuration file:
	a.	HTTPPortNumber
	b.	UseSSL
2.	If your IBM Planning Analytics instance uses a Self-Signed Certificate and UseSSL=T, additional configuration is required for Power BI Desktop and Power BI Service, as they work only with CA Certificates by default.
3.	Test the tm1 REST API connection by entering the following in a browser: http(s)://<Host>:<HTTPPortNumber>/api/v1/$metadata
4.	Start Performance Monitor. Without it running, some analytical information will not be available.

# Configuring Power BI
1.	If your IBM Planning Analytics instance uses a Self-Signed Certificate:
1.	Go to **File > Options and Settings > Security**. Set **Certificate Revocation** to **None**.
2.	To connect from Power BI Desktop, find the **Microsoft.Mashup.Container.NetFX45.exe.config** file in the installation directory of the program (and a similar file in the installation directory of the On-premises Data Gateway, if used for Power BI Service) and add the following settings:

```xml
<configuration>
  <system.net>
    <settings>
      <servicePointManager
        checkCertificateName="false"
        checkCertificateRevocationList="false"         
      />
    </settings>
  </system.net>
</configuration>
```

3.	Restart PA Model Explorer if it is open.

# Configuring Planning Analytics Model Explorer
Connection parameters for PA Model Explorer to the tm1 server are located in the text boxes on the first page of the program. In the navigation menu, select **Dashboard**.

# User Privileges
1.	The user connecting to the tm1 server must have **read** access to the model and control objects.
2.	It is highly recommended that the user does not have a maximum connection limit (**MaximumPorts**) to avoid the **ClientMaximumPortsExceeded** error.
