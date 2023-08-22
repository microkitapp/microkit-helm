# MicroKit Helm Repository Documentation

The MicroKit Helm repository provides Helm charts for deploying the MicroKit application. This documentation will guide you through the process of adding the MicroKit Helm repository, exploring chart values, and customizing the deployment using Helm.

## Adding the MicroKit Helm Repository

To add the MicroKit Helm repository to your Helm client, use the following command:

```bash
helm repo add microkit https://microkitapp.github.io/microkit-helm
```

## Exploring Chart Values

The MicroKit Helm chart provides a set of customizable values that allow you to configure the deployment according to your requirements. You can inspect these values using the following command:

```bash
helm show values microkit/microkit > values.yaml
```

This command will generate a `values.yaml` file in your current directory, containing the default configuration values for the MicroKit chart.

## Edit values.yaml And Customizing Secrets

The MicroKit Helm chart uses an encryption key for secure your data. You can customize this key and other secrets by following these steps:



2. Edit the `values.yaml` file:

Run those command in the 
```bash
sed -i '' "s|aes_key.*|aes_key\: $(openssl rand -base64 32)|" values.yaml

sed -i '' "s|password: postgres|password\: $(openssl rand -base64 24)|" values.yaml

sed -i '' "s|password: redis|password\: $(openssl rand -base64 24)|" values.yaml
```

Replace `YOUR_NEW_ENCRYPTION_KEY` with the encryption key generated in step 1.

## Disabling Redis and PostgreSQL

The MicroKit Helm chart enables Redis and PostgreSQL components by default. If you want to use your own Postgres/Redis , you can adjust the `values.yaml` file as follows:

### Disabling Redis:

To disable Redis, set the `redis.enabled` value to `false` in the `values.yaml` file:

Please be aware that you still need to specify Redis/PostgreSQL parameters for your Redis/PostgreSQL instance.


```yaml
redis:
  enabled: false
  host: REDIS_HOSTNAME
  port: REDIS_PORT
  password: REDIS_PASSWORD
```
Replace `REDIS_HOSTNAME`, `REDIS_PORT`, and `REDIS_PASSWORD` with your desired Redis configuration.

### Disabling PostgreSQL:

To disable PostgreSQL, set the `postgresql.enabled` value to `false` in the `values.yaml` file:

```yaml
postgres:
  enabled: false
  username: DB_USER
  dbhost: DB_HOST
  password: DB_PASSWORD 
  dbname: DB_NAME
```



Replace `DB_HOST`, `DB_NAME`, `DB_USER`, and `DB_PASSWORD` with your desired PostgreSQL configuration.



## Deploying MicroKit with Customized Values

Once you have customized the values in the `values.yaml` file, you can deploy the MicroKit application using the Helm chart with your custom configurations. Use the following command:

```bash
helm install microkit microkit/microkit -f values.yaml
```

This command will deploy the MicroKit application using the specified values from the `values.yaml` file.

## Updating and Managing the Deployment

You can update and manage your MicroKit deployment using standard Helm commands, such as `helm upgrade`, `helm rollback`, and `helm uninstall`. Refer to the Helm documentation for more information on these commands and their usage.

For further assistance or information, you can refer to the official MicroKit Helm repository: [https://microkitapp.github.io/microkit-helm](https://microkitapp.github.io/microkit-helm).

## Conclusion

Congratulations! You've successfully learned how to add the MicroKit Helm repository, explore chart values, customize the encryption key, and deploy the MicroKit application using Helm. This documentation provides a solid foundation for deploying MicroKit with customized configurations.