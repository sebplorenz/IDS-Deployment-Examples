<h1 align="center">
  <br>
  <a href="https://dataspace-connector.de/dsc_logo.svg"><img src="https://dataspace-connector.de/dsc_logo.svg" alt="Dataspace Connector Logo" width="200"></a>
  <br>
      Dataspace Connector - Full Setup
  <br>
</h1>

This is a deployment example for the **Full Setup** of the Dataspace Connector. It allows the exploration of all holistic functionalities of the Dataspace Connector and its services. 

---

**Note**: 
This example can not be used with the current IDS Metadata Broker and IDS AppStore off-the-shelf as a valid IDS identity certificate is not included. 
To get and install your own IDS identity certificate, please read the provided [documentation](https://international-data-spaces-association.github.io/DataspaceConnector/).

---

In this setup, the [Dataspace Connector](https://github.com/International-Data-Spaces-Association/DataspaceConnector) is started with the listed extensions:
* [Dataspace Connector UI](https://github.com/International-Data-Spaces-Association/DataspaceConnectorUI), 
* Portainer
* PostgreSQL DB

### Components & Versions
This deployment example builds on the following compatible versions:

| Component | Version |
|:----------|:--------|
| Dataspace Connector | 6.3.1 |
| Dataspace Connector UI | 8.6.0 |
| Portainer | 2.6.2 |
| PostgreSQL | 13 |

### Prerequisites
  - Git
  - Docker
  - Docker Compose

### Installation Steps
1. Clone the IDS Deployment Examples GitHub repository.
    ```
    git clone https://github.com/International-Data-Spaces-Association/IDS-Deployment-Examples.git
    ```
2. Open a new terminal inside the created directory and navigate to this folder.
    ```
    cd IDS-Deployment-Examples/dataspace-connector/full
    ```
3. Use a Docker Compose command to start all of the component's Docker containers, will pull images if not already existing.
   ```
   docker-compose up
   ```    
   - [PostgreSQL Note]: If the example should have already been setup locally in an older version before Dataspace Connector 6.0.0, 
     the `dataspaceconnector-data` volume must be deleted, since it was initially created with PostgreSQL 12 and is 
     thus incompatible with PostgreSQL 13. 
     The complete volume name can be found by: `docker volume ls` and should start with `dataspaceconnector-data`. 
     It can be removed by `docker volume rm <name>`.
   - [Portainer Note]: Portainer is in this example to enable IDS-App deployment into the connector from an IDS-AppStore. If no use of IDS-Apps is intended, Portainer can be removed from the docker-compose configuration.
   - [Portainer Note]: If no admin account is created in Portainer via the Portainer-UI within 5 minutes after starting the container, Portainer will automatically restart itself in this example.
   - [Portainer Note]: If use of IDS-Apps is intended, the Portainer settings must first be adjusted in the dataspaceconnector.env file and after starting the example a matching admin account and endpoint must be created via the Portainer-UI.
   - [Connector Note]: This example does not have the ids:connectorProxy entry in the connector configuration set. If a proxy is to be used, it must first be added to the connector configuration.
   
4. After all systems have been booted, they can be reached (by default) at the following URLs:
   - Dataspace Connector Swagger UI: https://localhost:8080/api/docs
     - Basic-Auth default credentials: username = admin, password = password
   - Dataspace Connector UI: http://localhost:8083/#/dashboard
   - Portainer UI: http://localhost:9000
     - Username and password must be set on first initialization. These have to be identical to the credentials provided in the Dataspace Connector .env file for Portainer communication.
     - Docker Endpoint must be provided next, either via the Portainer initialization dialog or later via the endpoint settings.

Individual settings can be provided via the `.env-files` of the respective components and via the `config.json` in `/dataspaceconnector/config/`, see the provided [documentation](https://international-data-spaces-association.github.io/DataspaceConnector/).

### Stop & Uninstall
  - Run `docker-compose down` inside the same folder you started the Dataspace Connector
  - Remove the repository folder

### Developers
This is an ongoing project of the developers of the Dataspace Connector repositories:
* [Dataspace Connector](https://github.com/International-Data-Spaces-Association/DataspaceConnector)
* [Dataspace Connector UI](https://github.com/International-Data-Spaces-Association/DataspaceConnectorUI)
