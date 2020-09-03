# Elastic IP Cleanup


```python
def elastic_ips_cleanup():
    """ Cleanup elastic IPs that are not being used """
    client = boto3.client('ec2')
    addresses_dict = client.describe_addresses()
    for eip_dict in addresses_dict['Addresses']:
        if "InstanceId" not in eip_dict:
            print (eip_dict['PublicIp'] +
                   " doesn't have any instances associated, releasing")
            client.release_address(AllocationId=eip_dict['AllocationId'])
```
