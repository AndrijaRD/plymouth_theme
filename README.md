# plymouth_theme
Custom plymouth boot splash screen theme. FBI inspired. 

This theme is made for arch linux with luks encryption that follows the grub loader with splash screen of:
 - FBI logo (watermark.png)
 - Gray box which contains lock.png and entry.png (entry is a placeholder for password)
 - Custom text that says "Enter your decryption passphrase."
 - Loading bar from progress_box.png filled with progress_par.png

One of the features is that while password is being typed bullet icons appear in entry.png, going from the middle to je sides (they are dinamicly centered).
After the password has been entered, the dialog options are hidden and on the screen remain only logo and progress bar.

To setup this theme place the files into `/usr/share/plymouth/themes/script` and then set plymouth theme to script:

`sudo plymouth-set-default-theme -R script`

# To setup the entier plymouth on the new system follow these steps:
 - `yay -S plymouth`
 - Open mkinitcpio `nano /etc/mkinitcpio.conf`
 - In MODULES line add `i915` for Intel GPUs, `amdgpu` for AMD GPUs and `nvidia nvidia_modeset nvidia_uvm nvidia_drm` for Nividia GPUs.
 - In the HOOKS line add `plymouth` (after the base udev)
 - Save and exit the file
 - Open grub fiile `nano /etc/default/grub`
 - In the GRUB_CMDLINE_LINUX_DEFAULT add `splash udev.log_priority=3 vt.global_cursor_default=1` after the `loglevel=3 quiet`
 - Save and exit the file
 - Reconfigure mk initcpio: `sudo mkinitcpio -P linux`
 - Then regenerate grub config on all locations using `sudo grub-mkconfig -o <path>`, path is usually `/boot/grub/grub.cfg` and `/boot/ufi/EFI/arch/grub.cfg`
   (So the command would need to runned twice, also the exact path may be different but it follows the simular pattern as the example)
 - After that plymouth is ready now just set the prefered theme.
 - To view available themes run `sudo plymouth-set-default-theme -l`
 - To set a theme run `sudo plymouth-set-default-theme -R <theme>`

*All of the theme files can be found in `/usr/share/plymouth/themes`*
