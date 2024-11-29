# Automating EDR Compliance with Tines
NIST updated the [Cybersecurity Framework (CSF)](https://www.nist.gov/cyberframework).  They introduced the Govern function as the glue to the other functions of risk management:
- Identify,
- Protect,
- Detect,
- Respond,
- and Recover.

Governance means creating a framework taliored to support the organization's critical mission. To ensure an organization can operate in a cyber or physical incident, infosec policies and standards are created to reduce cyber risk or business risk.  Compliance is the means to ensure adherence to the infosec standards and policies.

To assit with IT departments with EDR compliance, I created a web form where an IT admin or infosec analyst can upload a csv with hostnames to check to see if they are present in the CrowdStrike Falcon platform.

In addition, hosts are tagged with the departmental ID, so the hosts are incorporated into the CrowdStrike Fusion Workflows for vulnerability reporting and alert notification for host detections by the Falcon sensor.

