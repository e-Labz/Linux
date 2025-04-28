# Virsh (KVM/QEMU) - Principais Comandos

O virsh é uma ferramenta de linha de comando para gerenciar máquinas virtuais em ambientes KVM/QEMU.

## Listar Máquinas Virtuais

```bash
# Listar todas as VMs em execução
virsh list

# Listar todas as VMs (incluindo as desligadas)
virsh list --all
```

## Gerenciamento Básico de VMs

```bash
# Iniciar uma VM
virsh start nome_da_vm

# Desligar uma VM (shutdown normal)
virsh shutdown nome_da_vm

# Forçar desligamento (equivalente a desconectar a energia)
virsh destroy nome_da_vm

# Reiniciar uma VM
virsh reboot nome_da_vm

# Suspender uma VM
virsh suspend nome_da_vm

# Retomar uma VM suspensa
virsh resume nome_da_vm
```

## Acessar Console da VM

```bash
# Abrir console gráfico (requer instalação do virt-viewer)
virsh virt-viewer nome_da_vm

# Acessar console via texto
virsh console nome_da_vm
```

## Gerenciamento de Snapshots

```bash
# Criar snapshot
virsh snapshot-create-as nome_da_vm nome_do_snapshot "Descrição do snapshot"

# Listar snapshots de uma VM
virsh snapshot-list nome_da_vm

# Reverter VM para um snapshot
virsh snapshot-revert nome_da_vm nome_do_snapshot

# Excluir snapshot
virsh snapshot-delete nome_da_vm nome_do_snapshot
```

## Informações sobre as VMs

```bash
# Mostrar informações de uma VM
virsh dominfo nome_da_vm

# Ver configuração XML completa
virsh dumpxml nome_da_vm

# Ver informações sobre uso de CPU
virsh cpu-stats nome_da_vm

# Ver estatísticas de memória
virsh dommemstat nome_da_vm
```

## Edição de Configurações

```bash
# Editar configuração XML da VM
virsh edit nome_da_vm

# Alterar número de vCPUs (VM precisa estar desligada)
virsh setvcpus nome_da_vm 4 --config

# Alterar memória (em KiB, VM precisa estar desligada)
virsh setmaxmem nome_da_vm 4194304 --config  # 4GB
```

## Gestão de Armazenamento

```bash
# Listar pools de armazenamento
virsh pool-list --all

# Listar volumes em um pool
virsh vol-list default

# Criar um novo volume
virsh vol-create-as default novo_disco 10G

# Anexar disco a uma VM
virsh attach-disk nome_da_vm /caminho/para/imagem.qcow2 vdb --cache none
```

## Gestão de Redes

```bash
# Listar redes virtuais
virsh net-list --all

# Ver detalhes de uma rede
virsh net-info default

# Iniciar uma rede
virsh net-start nome_da_rede

# Desativar uma rede
virsh net-destroy nome_da_rede
```

## Migração de VMs

```bash
# Migrar VM para outro host (migração ao vivo)
virsh migrate --live nome_da_vm qemu+ssh://destino/system
```

## Clonagem e Criação de VMs

```bash
# Clonar uma VM existente
virt-clone --original nome_da_vm_original --name nova_vm --auto-clone

# Criar VM a partir de um arquivo XML
virsh define /caminho/para/arquivo.xml
```
