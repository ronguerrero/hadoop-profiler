# Hadoop Profiler

>### 1. About Hadoop Profiler
Hadoop Profiler is a Migration Assessment Tool to profile and generate metrics out of YARN (which is the primary resource management and scheduling tech on Hadoop). These metrics could be useful to understand  applications that are running in an hadoop environment and generate insights into migration strategies.

>### 2. Overview
The Profiler consists of a simple shell script, [profiler.sh](Profiler/profiler.sh) which extracts data from YARN, Ambari or Cloudera Manager. This script takes required configuration values from a configuration file, [profiler.conf](Profiler/profiler.conf) which needs to be updated with required values before the execution.

#### Metrics/Information extracted from a Hadoop Cluster
1. YARN Application execution metrics, Host details and scheduler information.
2. Spark History Server Metrics. 
3. CDH Specific information:
    - Services, Host and Components from Cloudera Manager (CM)
    - Impala logs based on the input dates 
4. HDP (or HD Insight) Specific information:
    - The blueprint, Services, Host and Components from Ambari
    - Ranger policies and Repos (incase Ranger is used)
    - NOTE: Set the HDI flag to Y or N if the distribution is Azure HD Insight. 
5. Other Distributions:
    - Only YARN and Spark History Server metrics are supported at this time.



#### Profiler Script Configutation

<table>
<tbody>
<tr>
<td>&nbsp;</td>
<td>
<p><strong>Properties</strong></p>
</td>
<td>
<p><strong>Description</strong></p>
</td>
</tr>

<tr>
<td rowspan="8">
<p><span style="font-weight: 400;">YARN Resource manager Configs</span></p>
</td>
<td>
<p><span style="font-weight: 400;">RM_SERVER_URL</span></p>
</td>
<td>
<p><span style="font-weight: 400;">YARN Resource manager URL. Comma separated URLs in case of HA&nbsp;</span></p>
<br />
<p><span style="font-weight: 400;">Use Cloudera Manager or Ambari, navigate to YARN, open Resource Manager and copy the host name from URL in your browser</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RM_SERVER_PORT</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Resource Manager Port&nbsp;</span></p>
<br />
<p><span style="font-weight: 400;">(see instructions above)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RM_SECURE</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is https enabled (Y/N)&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RM_KERBERIZED</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is Kerberized (Y/ N)&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">GOT_KEYTAB</span></p>
</td>
<td>
<p><span style="font-weight: 400;">To Automate the extract in case of a Kerberized Environment.</span></p>
<br />
<p><span style="font-weight: 400;">USE Y, if you want script to run kinit based on parameters below</span></p>
<br />
<p><span style="font-weight: 400;">USE N, if you already have a kerberos ticket active in the environment. (in this case, script will not try to do kini and you don't&nbsp; need kerberos settings below)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">KEYTAB_PATH</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Path to the Keytab file</span></p>
<br />
<p><span style="font-weight: 400;">(use only when GOT_KEYTAB=Y)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">KEYTAB</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Keytab file Name&nbsp;</span></p>
<br />
<p><span style="font-weight: 400;">(use only when GOT_KEYTAB=Y)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">PRINCIPAL</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Keytab Principal for Kinit&nbsp;</span></p>
<br />
<p><span style="font-weight: 400;">(use only when GOT_KEYTAB=Y)</span></p>
</td>
</tr>
<tr>
<td>
</tr>
<tr>
<td rowspan="8">
<p><span style="font-weight: 400;">Spark History Server Configs</span></p>
</td>
<td>
<p><span style="font-weight: 400;">SPARK_HS_URL</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Spark History Server URL. &nbsp;</span></p>
<br />
<p><span style="font-weight: 400;">Use Cloudera Manager or Ambari, navigate to Spark Service and copy the host name from URL in your browser</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">SPARK_HS_PORT</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Spark History Server Port &nbsp;</span></p>
<br />
<p><span style="font-weight: 400;">(see instructions above)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">SPARK_HS_SECURE</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is https enabled (Y/N)&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">SPARK_HS_KERBERIZED</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is Kerberized (Y/ N)&nbsp;</span></p>
</td>
</tr>
<tr>

</tr>
<tr>

</tr>
<tr>

</tr>
<tr>

</tr>
<tr>
<td>&nbsp;</td>
<td>
<p><span style="font-weight: 400;">DISTRIBUTION</span></p>
</td>
<td>
<p><span style="font-weight: 400;">On-Prem Distribution : HDP or CDH or OTH&nbsp;</span></p>
</td>
</tr>
<td rowspan="10">
<p><span style="font-weight: 400;">Cloudera Manager and Impala&nbsp; Related Configurations if the distribution is CDH</span></p>
</td>
<td>
<p><span style="font-weight: 400;">CM_SERVER_URL</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Cloudera Manager URL&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_SERVER_PORT</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Cloudera Manager Port&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_ADMIN_USER</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Cloudera Manager Admin User</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_ADMIN_PASSWORD</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Cloudera Manager Password&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_CLUSTER</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Cloudera Manager Cluster Name&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_API_VERSION</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Cloudera Manager API Version. Can be Obtained from CM UI. Click &ldquo;Support&rdquo; and &ldquo;API Documentation&rdquo;.&nbsp; API Version number should be available on this page (like v00)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_SECURED</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is https enabled for Cloudera Manager (Y/N)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_IMPALA_NUMBER_OF_DAYS</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Number of days for initial extraction</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CM_IMPALA_INTERVAL_MINUTES</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Number of minutes per json file extracted, options are 1, 2, 3, 6, 10, 20, 30, 60</span></p>
</td>
</tr><tr>
<td>
<p><span style="font-weight: 400;">CM_IMPALA_PAGES</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Number of pages to be extracted per file (interval), cloudera manager limits 1000 queries per page&nbsp;</span></p>
</td>
</tr>

<tr>
<td rowspan="12">
<p><span style="font-weight: 400;">Ambari and Ranger Related Configurations if the distribution is HDP&nbsp;</span></p>
</td>

<td>
<p><span style="font-weight: 400;">IS_HDI</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is the Distribution Azure HD Insight (Y/N)&nbsp;</span></p>
</td>
</tr>
<td>
<p><span style="font-weight: 400;">AMBARI_ADMIN_USERID</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Ambari Admin User id&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">AMBARI_ADMIN_PASSWORD</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Ambari Admin Password&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">AMBARI_SERVER</span></p>
</td>
<td>
<p><span style="font-weight: 400;">URL for Ambari Server&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">AMBARI_PORT</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Ambari Server Port&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">CLUSTER_NAME</span></p>
</td>
<td>
<p><span style="font-weight: 400;">HDP Cluster name&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">AMBARI_SECURED</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is https enabled on Ambari (Y/N)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">IS_RANGER_SETUP</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is Ranger enabled on the cluster (Y/N)&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RANGER_URL</span></p>
</td>
<td>
<p><span style="font-weight: 400;">URL for Ranger Admin&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RANGER_PORT</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Ranger Admin Port&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RANGER_SECURED</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Is https enabled for Ranger URL (Y/N)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RANGER_USER</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Ranger admin User&nbsp;</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">RANGER_PWD</span></p>
</td>
<td>
<p><span style="font-weight: 400;">Ranger admin Password&nbsp;</span></p>
</td>
</tr>
<tr>
</tbody>
</table>


>### 3. How to Run

**Initial Extraction :**  
It is recommended to run the first execution manualy to make sure correct configuration values.
Execute the following on the edge node or a host that can reach the YARN Resource Manager or Ambari or CM. 

1. git clone -b main https://github.com/databricks-migrations/hadoop-profiler.git
2. cd Profiler/Profiler
3. Update [profiler.conf](Profiler/profiler.conf) to required settings depending on your Hadoop distribution. The code automatically determines if its an Initial or Incremental Extract. 
3. chmod +x profiler.sh 
4. ./profiler.sh 
5. Make sure the Output extracts have the data extracted. 

**Daily extraction :**  
- Schedule profiler.sh to run daily for at least 2 weeks. 
- Frequency of Excution: YARN has a default log  aggregation and retention set as 10000 (yarn.resourcemanager.max-completed-applications)  and starts cleaning up the older application history. It is important to check this value and schedule the extracts appropriately to capture all the application. 
- Note:  At any given time, if there is a need to initial extract, delete the folder "ExtractTracker" with in the Profiler directory.  

>### 4. Output: 

All the extracts are stored as part of the Output Folder within their respective components Sub-folders.
