# Cloud Lab 4 — Amazon VPC with Public and Private Subnets

| Item | Details |
|---|---|
| Student name | Sam Nangalex |
| Student ID | e2022053 |
| AWS Region | US East (N. Virginia) (`us-east-1`) |


### 1. VPC

Created `lab4-vpc` with IPv4 CIDR `10.0.0.0/24`.

![VPC configuration](images/01-vpc.png)

### 2. Internet gateway

Created `lab4-internet-gateway` and attached it to `lab4-vpc`.

![Internet gateway attached to VPC](images/02-internet-gateway.png)

### 3. Public subnet

Created `lab4-public-subnet` with CIDR `10.0.0.0/25` in `us-east-1a`.

![Public subnet](images/03-public-subnet.png)

### 4. Public route table

Configured the public subnet route table with `0.0.0.0/0` pointing to `lab4-internet-gateway` and associated it with the public subnet.

![Public route table](images/04-public-route-table.png)

### 5. Public EC2 instance

Launched `lab4-ec2-01` in `lab4-public-subnet` with a public IPv4 address and the `LabInstanceProfile` instance profile.

![Public EC2 instance](images/05-ec2-public.png)

### 6. Public instance connectivity test

Ran `sudo yum update -y` on `lab4-ec2-01` using Systems Manager Run Command. The command completed successfully.

![Public instance Run Command result](images/06-test-public.png)

### 7. Private subnet

Created `lab4-private-subnet` with CIDR `10.0.0.128/25` in `us-east-1a`.

![Private subnet](images/07-private-subnet.png)

### 8. NAT gateway

Created `lab4-nat-gateway` in `lab4-public-subnet` and allocated an Elastic IP. Waited for the NAT gateway to become available.

![NAT gateway](images/08-nat-gateway.png)

### 9. Private route table

Created `lab4-custom-route-table`, added `0.0.0.0/0` pointing to `lab4-nat-gateway`, and associated it with `lab4-private-subnet`.

![Private route table](images/09-private-route-table.png)

### 10. Private EC2 instance

Launched `lab4-ec2-02` in `lab4-private-subnet` with auto-assigned public IP disabled and the `LabInstanceProfile` instance profile.

![Private EC2 instance](images/10-ec2-private.png)

### 11. Private instance connectivity test

Ran `sudo yum update -y` on `lab4-ec2-02` using Systems Manager Run Command. The command completed successfully through the NAT gateway, although the instance has no public IP address.

![Private instance Run Command result](images/11-test-private.png)

