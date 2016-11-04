FFIEC CDR Public Web Service Sample Client Readme

PURPOSE
This is a sample web service client for the FFIEC 
CDR Public Web Service.

DISCLAIMER
This sample web service client is intended to serve as an example to the users of the 
FFIEC Public Web Service for developing their own web service client applications and 
is presented only as an exhibit of the functionality of which the web service is capable.  
The sample client code itself is not supported and no guarantees are made or implied for 
its capabilities.  No questions can be answered about the design and implementation of 
this program.  Please use the code at your own discretion.

PREREQUISITES:
1) Microsoft .Net Framework 2.0
2) Microsoft Web Services Enhancements (WSE) 2.0 Service Pack 3
3) To re-create reference.sc file  - C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin>wsdl /out:reference.cs http://localhost/pdd/pws/WebServices/RetrievalService.asmx?wsdl
4) Right click Web references file FFIECPublicWebService to update the web reference after updating the web service project
5) Change System.Web.Services2.WebServicesClientProtocol to Microsoft.Web.Services2.WebServicesClientProtocol
6) Change using Microsoft.Web.Services.Protocols to Microsoft.Web.Services2


**************7.30.2016 Update********************************

1) download VS2010 express
2) download Microsoft Web Services Enhancements (WSE) 2.0 Service Pack 3
3) Add reference to Microsoft.Web.Services2
4) Delete web reference to FFIECPublicWebService
5) Add web reference back by adding service reference -> advanced options -> input web reference url -> https://cdr.ffiec.gov/public/pws/webservices/retrievalservice.asmx?wsdl
6) To re-create reference.cs file  
	A) Create c:\test
	B) From the command line, cd to C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Bin
	C) Once in the directory, run: wsdl.exe /out:C:\test\reference.cs https://cdr.ffiec.gov/public/pws/webservices/retrievalservice.asmx?wsdl
7) Open c:\test from file explorer, copy reference.cs and paste into C:\Users\chase\Desktop\EcommerceSampleWebClientSourceCodeGood\EcommerceSampleWebClientSourceCode\FFIECPublicWebServiceSampleClient\Web References\FFIECPublicWebService
8) Update web reference
9) Open app.config from solution explorer, replace contents with:

			<?xml version="1.0" encoding="utf-8"?>
			<configuration>
			  <configSections>
				<section name="microsoft.web.services3" type="Microsoft.Web.Services3.Configuration.WebServicesConfiguration, Microsoft.Web.Services3, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35"/>
				<sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089">
				  <section name="FFIECPublicWebServiceSampleClient.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" requirePermission="false"/>
				</sectionGroup>
			  </configSections>
			  <system.web>
				<webServices>
				  <!--<soapExtensionTypes>
					<add type="Microsoft.Web.Services3.WebServicesExtension, Microsoft.Web.Services3, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" priority="1"/>
				  </soapExtensionTypes> -->
				  <soapExtensionImporterTypes>
					<add type="Microsoft.Web.Services3.Description.WseExtensionImporter, Microsoft.Web.Services3, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" />
				  </soapExtensionImporterTypes>
				  <soapServerProtocolFactory type="Microsoft.Web.Services3.WseProtocolFactory, Microsoft.Web.Services3, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" />
				</webServices>
				<compilation>
				  <assemblies>
					<add assembly="Microsoft.Web.Services3, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35"/>
				  </assemblies>
				</compilation>
			  </system.web>
			  <microsoft.web.services3>
				<!-- Any WSE configuration settings go here -->
				<diagnostics/>
			  </microsoft.web.services3>
			  <applicationSettings>
				<FFIECPublicWebServiceSampleClient.Properties.Settings>
				  <setting name="FFIECPublicWebServiceSampleClient_FFIECPublicWebService_RetrievalService"
					serializeAs="String">
					<value>https://cdr.ffiec.gov/public/pws/webservices/retrievalservice.asmx</value>
				  </setting>
				</FFIECPublicWebServiceSampleClient.Properties.Settings>
			  </applicationSettings>
			  <startup>
				<supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5"/>
			  </startup>
			</configuration>
			
10) Open FacsimileRetrievalForm.CS and replace using with:

			using System;
			using System.Drawing;
			using System.Collections;
			using System.Collections.Specialized;
			using System.ComponentModel;
			using System.Windows.Forms;
			using System.Data;
			using System.IO;
			using System.Web.Services;
			using System.Web.Services.Protocols;
			using System.Xml;
			using System.Timers;

			using Microsoft.Web.Services2;
			using Microsoft.Web.Services2.Security;
			using Microsoft.Web.Services2.Security.Tokens;

11) Compile 