# CAPTCHA Usage Documentation

## Related Documentation
- [Link1]
- [Link2]
- [Link3]
- [Link4]

## Overview

CAPTCHA is a security mechanism aimed at distinguishing legitimate users from automated bots or bad actors. It helps protect the service from spam and malicious activity.

A CAPTCHA is not shown on every interaction, as that has a negative impact on user experience. For our service, it can be triggered in five separate ways. **Triggering any one rule results in a CAPTCHA.** 

## Triggers

1. High request volume from a single IP address
    
    - **Reason:** Detects automated traffic from a single source.
    - **Condition:** If more than 500 requests have been received from the same IP address in less than 20 minutes. 

2. Blacklisted IP address
    
    - **Reason:** Acts as additional identification for IP addresses that were labeled as suspicious in the past.
    - **Condition:** If the IP address from which the request is received is found in the blacklist.

3. Unusual request volume
    
    - **Reason:** Protects the service during an abnormal spike in traffic (_could_ indicate coordinated attack or automated activity).
    - **Condition:** If the service receives more than double average requests for the last 2 weeks in the current hour bucket.

4. Repeated payload in short time interval
    
    - **Reason:** Detects attempts at brute-forcing access to the system.
    - **Condition:** If the same payload has been sent more than 5 times in the last 30 seconds.

5. Manually enabled CAPTCHA
    
    - **Reason:** Allows administrators to temporarily increase service security.
    - **Condition:** If the CAPTCHA has been enabled manually via admin panel for certain requests. 

## Troubleshooting

In the case users report unexpected CAPTCHA prompts, follow these steps:

1. Check the overall request volume
    - If it exceeds double the average requests in the past two weeks, it may be expected.

2. Check for manually enabled CAPTCHA
    - Confirm whether the mechanism was enabled by another admin.

3. Check for IP specific request volume
    - Does the affected IP address have more than 500 requests in less than 20 minutes?

4. Check the IP's blacklist status
    - Verify if the IP address is blacklisted.

5. Check for repeated payloads
    - Identify if identical payloads are repeatedly submitted.

### Warning: If there is a large volume of CAPTCHAS with no discernable cause for longer than 20 minutes, contact security.
