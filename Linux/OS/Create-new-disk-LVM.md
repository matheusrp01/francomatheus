# Criando discos no formato de LVM 💿

O formato de disco LVM (*Logical Volume Manager*) trouxe uma flexibilidade muito grande para quem administra servidores Linux, isso porque este tipo de disco traz uma simplicidade muito grande para expandir volumes.
Com o LVM já criado bastaria a gente executar apenas 3 comandos para expandir uma partição.

## E como criamos uma partição LVM?

1. Adicione o novo disco na máquina (seja virtual ou física).
2. Execute o comando para listar os discos:

``` 
fdisk -l
```

3. Seu novo disco será `/dev/sdb` (caso já não tenha discos adicionais)
4. Execute o comando para iniciar a formatação do disco:

```
fdisk /dev/sdb
```
5. Pressione `n` para criar uma partição, `p` para selecionar partição primária e `w` para salvar as alterações.
6. Execute novamente o comando do passo 2 e veja se o disco `/dev/sdb` está na lista com uma partição `/dev/sdb1`.
7. Depois de validar, vamos criar um *Physical Volume* (pv):

```
pvcreate /dev/sdb1
```
8. Agora vamos criar um *Volume Group* do *pv* criado:

```
vgcreate files_VG /dev/sdb1
```
9. Valide se o *vg* foi criado:

```
vgdisplay files_VG
```
10. Após validar, vamos criar um *Logical Volume* (lv):

```
lvcreate -n lv_files --size 50G files_VG
```
11. Valide se o *lv* foi criado:

```
lvdisplay lv_files
```

12. Após validar, vamos formatar como ext4:

```
mkfs.ext4 /dev/files_VG/lv_files
```

13. Finalmente nossa partição está com o *file system* para armazenar arquivos. Agora vamos montar a nova partição para uma nova pasta dentro do OS:

```
mkdir /files;
mount /dev/files_VG/lv_files /files;
```

14. Pronto. Caso você queira deixar montado a partição, adicione no arquivo `/etc/fstab` os parâmetros abaixo:

```
/dev/files_VG/lv_files   /files        ext4   defaults        0 1
```

#### Este caso é apenas para discos novos com novas partições. O procedimento para expandir uma nova partição é outro.
