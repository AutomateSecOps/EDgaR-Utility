# Automating EDR Compliance with Tines
NIST updated the Cybersecurity Framework (CSF).  They introduced the Govern function as the glue to the other functions of risk management:
- Identify,
- Protect,
- Detect,
- Respond,
- and Recover.

Governance creates a framework taliored to support the organization's critical mission. To ensure daily operations in the event of a cyber incident, business continuity plans, infosec policies and standards are created for resiliency.  Cyber risk management provides a means to manage business risk.  Compliance is the means to ensure adherence to the infosec standards and policies.

To assit with IT departments with EDR compliance, my teammate and I created a web form where an IT admin or infosec analyst, who does not have access to the CrowdStrike console, can upload a csv with hostnames to check to see if the host is present in the CrowdStrike Falcon platform.

In addition, hosts are tagged with the departmental ID, so the hosts are incorporated into the CrowdStrike Fusion Workflows for vulnerability reporting and for alert notification on host detections by the Falcon sensor.

 The workflows are straightforward using the Tines CrowdStrike templates for the Get host IDs, Get Host details, and Tag Host in CrowdStrike, which are available in the Tines product templates.
### AI Automatic Mode to Strip the FQDN of the hostname
The hostnames are parsed from the csv, and each hostname is exploded as an individual event.  Since the CrowdStrike /devices/queries/devices/v1 API endpoint for host management has a quirk in regards to fully qualified domain names (FQDN), we used the Tines AI Automatic mode in Event Transformation action to strip the hostname of the FQDN.

<img src="./images/AI-Automatic-Mode-StripFQDN.png">

If an analyst submits a host with a FQDN, and the host is registered without a FQDN, CrowdStrike Host API will not find the host.  The API will return a FQDN if searching just by the host name.

For example, host1.mydomain.com is registered in the console.  The Falcon API will return it if the hostname submitted as host1 or host1.mydomain.com, but if host1.mydomain.com is submitted and host1 is registered, the Falcon Host API will not find it.

### CrowdStrike Tagging Trigger Logic

In the webform, the analyst or IT admin can enter 3 tags for a host:

<img src="./images/CS-Tagging-Webform.png">

If all three tags are not used, the CrowdStrike Host API will create a blank FalconGrouping tag on the host.  In order to bypass the blank tag, we created a trigger logic based on the number of tags used.  The first trigger logic used this formula:

<img src="./images/Trigger-MoreThan1tag.png">

If there was only one tag, it would follow the No Match pathway for one tag.

If it was true, then the workflow continued to the second trigger action to determine if three tags were used:

<img src="./images/Trigger-MoreThan2tag.png">

If false, the workflow continued to the CrowdStrike Tag host action with the two tags.  If three tags were used, the workflow continued to the three tag CrowdStrike action:

<img src="./images/Tag-3Hosts-In-CS.png">

In short, EDR compliance is challenging. With the Tines automation platform, you can save time and resources by providing a webform for IT departments to check if the CrowdStrike Falcon Sensor is registred and tagged properly. 

I hope you found this useful.

Once you start automating, you cannot stop!

Happy Building.

Tom

## Tines Documenation
- [Tines AI Automatic Mode Event Transformation](https://www.tines.com/docs/actions/types/event-transformation/automatic//)
- [Tines IS PRESENT Function](https://www.tines.com/docs/formulas/functions/is-present/)
- [Tines Object Function](https://www.tines.com/docs/formulas/functions/object/)
- [Tines Append Function](https://www.tines.com/docs/formulas/functions/append/)
- [Tines Append Element to Resource](https://www.tines.com/api/resources/append-element/)
- [Tines Pages](https://www.tines.com/docs/pages/)
- [Tines Community Edition](https://www.tines.com/pricing/)

## NIST
- [CSF](https://www.nist.gov/cyberframework)

[Previous Blog](https://working-with-tines-resources.automatesecops.com/)
