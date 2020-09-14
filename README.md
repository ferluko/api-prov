# StackStorm Comafi Pack
Paquete de instalación de Stackstorm del proyecto IaC para aprovisionamiento de infraestructura.

## Introducción
En el corriente repositorio se encuentran los fuentes necesarios para desplegar las acciones y sus manifiestos, los sensores, los workflows y las reglas de la plataforma Stackstorm del proyecto IaC para aprovisionamiento de infraestructura.

### Pre-Requisitos
_En tu entorno._
* [Stackstorm:]() Instancia con todos sus servicios desplegada y cliente CLI ```st2``` instalado.
* []()

## Instalación de StackStorm
#### Quick Install Bare Metal (Linux)

Grab a clean 64-bit Linux system that fits the system requirements. Make sure that curl is up to date using sudo apt-get install curl on Ubuntu, or sudo yum install curl nss on RHEL/CentOS. Then run this command:
```
curl -sSL https://stackstorm.com/packages/install.sh | bash -s -- --user=st2admin --password='Ch@ngeMe'
```
Documentación: https://docs.stackstorm.com/install/index.html

## Instalación del pack
```
st2 pack install https://github.com/ferluko/api-prov
```


### ST2 Client
```
st2 --version

# Get help. There's a lot to explore.
st2 -h

# Login - add "-w" to save the password if you like
# st2admin/Ch@ngeMe is the default username & password. Replace if needed
st2 login st2admin -p 'Ch@ngeMe'

# List the actions from the 'core' pack
st2 action list --pack=core
st2 trigger list
st2 rule list

# Run a local shell command
st2 run core.local -- date -R

# List of executions (most recent at the bottom)
st2 execution list

# Get execution by ID
st2 execution get <execution_id>

# Get only the last 5 executions
st2 execution list -n 5

# Make an API Key
st2 apikey create -k -m '{"used_by": "api test"}'

# Copy examples to st2 content directory and set permissions
sudo cp -r /usr/share/doc/st2/examples/ /opt/stackstorm/packs/
sudo chown -R root:st2packs /opt/stackstorm/packs/examples
sudo chmod -R g+w /opt/stackstorm/packs/examples

# Run setup
st2 run packs.setup_virtualenv packs=examples

# Reload stackstorm context
st2ctl reload --register-all
```

### API REST
[StackStorm API Docs](https://api.stackstorm.com/) 
Comandos:
```
curl -k -H "St2-Api-Key: <API Key>" https://<St2_server>/api/v1/actions/<nombre de paquete>.<nombre de acción> |jq 

curl -k -H "St2-Api-Key: <API Key>" https://<St2_server>/api/v1/apikeys

```

### Webhook
#### Ejecución de Webhook ```sample```
```
curl -k https://localhost/api/v1/webhooks/sample -d '{"foo": "ferluko desde webhook", "name": "st2"}' -H 'Content-Type: application/json' -H 'St2-Api-Key: MDZmYWNmYzRhYmZlMzRkNDVkNWM4YTBlMDFkNWQxNmJhYTg2NDkwZGJmZGUwNTI5ZGZkNGQzNWNlZGY2ZjEyMw'
```

