# Key Management

## Introduction

A _Vault_ in OCI is a secure container used to store and manage _Encryption Keys_ and _Secrets_, offering options like Standard or Virtual Private Vaults for different security and isolation needs. 
A _Master Encryption Key_ is a key stored in the _Vault_, used to encrypt and decrypt data encryption keys or directly protect sensitive data. 

In this lab you create the required OCI resources to use a customer-managed key for data-at-rest encryption in Object Storage and 
Block Volume.

Estimated Time: 30 minutes

### About Vault

OCI Vault is a secure service designed to centrally manage encryption keys and secrets, ensuring robust data protection and compliance. It supports customer-managed keys (CMKs), Oracle-managed keys, and Bring Your Own Key (BYOK) for full control over key lifecycle management. Encryption keys stored in the vault enable seamless integration with OCI services, providing encryption for data at rest and in transit with fine-grained access control.


### Objectives

In this lab, you will:

* Create a Vault
* Create a Master Encryption Key
* Create a private Object Storage bucket with a custom-managed key
* Change the encryption key of a Block Volume to a customer-managed key

### Prerequisites (Optional)

This lab assumes you have:
* An Oracle Cloud account
* All previous labs successfully completed

## Task 1: Create Vault

1. Click the Navigation Menu in the upper left, navigate to Identity & Security, and select Vault. Select the compartment you are assigned to (check which compartment you are assigned where you have provisioned the Livelabs resources).

	![OCI Console Screen Vault Dashboard Emtpy](images/basic-create-vault-dashboard-empty.png " ")

2. Click **Create Vault**. We create a new Vault for this lab.

	![Empty Vault Detail Page](images/basic-create-vault-detail-empty.png " ")

3. Insert Vault name, as example _vault-livelab_. Do *NOT* enable private vault. Click on **Create Vault**, the vault is provisioned.

	![Filled Vault Detail Page with Vault Name](images/basic-create-vault-detail-filled.png " ")

4. Verify the new created _Vault_. The state changes after some minutes from _Creating_ to _Active_.

	![OCI Console Screen Vault Dashboard Vault listed](images/basic-create-vault-dashboard-filled.png " ")

## Task 2: Create Master Encryption Key

1. In _Vault_ start page, select the previous created _Vault_, click on the **name** of the Vault to see the details.

	![OCI Console Screen Vault Dashboard Vault listed](images/basic-create-vault-dashboard-filled.png " ")

2. Scroll at the bottom of the _Vault_ screen. In section _Master Encryption Keys_, create a new Master Encryption key. Click on **Create Key**.

	![OCI Console Screen Master Encryption Key Dashboard empty](images/basic-create-mek-dashboard-empty.png " ")

3. In **Create Key** screen, we add the information to create a new _Master Encryption Key_. Use this values:

    - **Protection Mode**: Software - __*Attention: HSM is fee-based, use Software instead!*__
    - **Name**: mek-livelab
    - **Key Shape: Algorithm**: AES
    - **Key Shape: Length**: 256 bits

	![Master Encryption Key Detail Page with Protection mode and Name set](images/basic-create-mek-detail-filled.png " ")

  Click on **Create Key** to create the _Master Encryption Key_.   

4. Verify the new created _Master Encryption Key_. The state changes after some minutes from _Creating_ to _Active_. The _Master Encryption Key_ is ready to use in other resources.

	![OCI Console Screen Master Encryption Key Dashboard listed](images/basic-create-mek-dashboard-filled.png " ")

## Task 3: Create private Object Storage bucket with the Master Encryption Key

1. Click the Navigation Menu in the upper left, navigate to Storage, and select Buckets. Select the compartment you are assigned to (check which compartment you are assigned where you have provisioned the Livelabs resources).

	![OCI Console Object Storage Dashboard empty](images/basic-object_storage-dashboard-empty.png " ")

2. Click **Create Bucket**. We create a new private Object Storage bucket for this lab.

	![Empty Object Storage Detail Page](images/basic-object_storage-dashboard-create.png " ")

3. In **Create Bucket** screen, we add the information to create a new _Object Storage bucket_. Use this values:

    - **Bucket Name**: private_bucket_livelab
    - **Encryption**: Select Encrypt using customer-managed keys
    - **Vault in [your compartment]**: Select created _Vault_
    - **Master Encryprion Key in [your compartment]**: Select created Master Encryption Key

	![Object Storage Detail Page with Name, Vault and Master Encryption Key set upper screen](images/basic-create-object-storage-detail-filled-upper.png " ")

	![Object Storage Detail Page with Name, Vault and Master Encryption Key lower screen](images/basic-create-object-storage-detail-filled-lower.png " ")
  Click on **Create** to create the _Object Storage bucket_ with the selected _Master Encryption Key_.   

4. Verify the new created _Object Storage bucket_.

	![OCI Console Screen Master Encryption Key Dashboard listed](images/basic-create-object-storage-dashboard-filled.png " ")

5. Click on the Objet storage name to verify new _Master Encryption Key_ is used.

	![OCI Console Screen Object Storage bucket detail page](images/basic-create-object-storage-detail_view.png " ")

## Task 4: Change Block Volume Master Encryption Key

1. Click the Navigation Menu in the upper left, navigate to Compute, and select Instance. Select the compartment you are assigned to (check which compartment you are assigned where you have provisioned the Livelabs resources). Two compute instances are listed.

	![OCI Console Screen Compute Instance Dashboard](images/basic-compute-instance-dashboard-filled.png " ")

2. Select the _webserver01_ instance by click on the instance name.

	![OCI Console Screen Compute Instance Selection](images/basic-compute-instance-dashboard-select.png " ")

3. In the left _Resources_ column, click on **Boot volume** to see the current attached Boot Volume.

	![OCI Console Screen Compute Instance Resource Boot Volume Selection](images/basic-compute-instance-dashboard-boot-volume-select.png " ")

4. Click on **Boot volume name** to get the specifications of the Boot Volume.

	![OCI Console Screen Compute Instance Resource Boot Volume Details](images/basic-compute-instance-dashboard-boot-volume-details-get.png " ")

5. At the Boot Volume specification page in _Encryption key_ section, click on **Assign**.

	![OCI Console Screen Compute Instance Resource Boot Volume KEy Assignment](images/basic-compute-instance-dashboard-boot-volume-details-assign.png " ")

6. Select your _Vault_ and _Master Encryption Key_, click on **Assign**. You  don't see the vault? Verify the compartment first. The Boot Volume changes state temporarily _PROVISIONING_. 

	![OCI Console Screen Boot Volume Encryption Key Assignment Screen](images/basic-compute-instance-dashboard-boot-volume-details-assign-confirm.png " ")

7. Verify new **Encryption key** is set.

	![OCI Console Screen Compute Instance Boot Volume with new Encryption Key](images/basic-compute-instance-dashboard-boot-volume-verification.png " ")


## Learn More

* [Oracle Cloud Infrastructure Documentation - Vault Start Page](https://docs.oracle.com/en-us/iaas/Content/KeyManagement/home.htm).

## Acknowledgements
* **Author** - <Name, Title, Group>
* **Contributors** -  <Name, Group> -- optional
* **Last Updated By/Date** - <Name, Month Year>
