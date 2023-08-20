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

## Customizing Encryption Key

The MicroKit Helm chart uses an encryption key for secure communication. You can customize this key by following these steps:

1. Generate a new encryption key using the `openssl` command:

```bash
openssl rand -base64 32
```

2. Edit the `values.yaml` file:

Use your preferred text editor to open the `values.yaml` file generated earlier.

3. Locate the `aes_key` value within the `values.yaml` file.

4. Replace the existing `aes_key` value with the newly generated encryption key.

For example, you can use the `sed` command to automate this process:

```bash
sed -i '' "s|aes_key.*|aes_key\: YOUR_NEW_ENCRYPTION_KEY|" values.yaml
```

Replace `YOUR_NEW_ENCRYPTION_KEY` with the encryption key generated in step 1.

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