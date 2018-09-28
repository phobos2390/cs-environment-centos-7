Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  config.vm.provider :virtualbox do |vb|
    vb.memory = 4096
  end

  #config.vm.provision :shell, name: "Setup-Display", privileged: false, inline: <<-SHELL
  #  export DISPLAY="#{ENV['DISPLAY']}"
  #  echo "export DISPLAY='$DISPLAY'" >> /home/vagrant/.bash_profile
  #SHELL
  config.vm.provision :shell, name: "yum-downloads", privileged: false, inline: <<-SHELL
    sudo rpm --import "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF"
    sudo curl https://download.mono-project.com/repo/centos7-stable.repo -Lo /etc/yum.repos.d/mono-centos7-stable.repo

    sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'

    sudo yum install -y mono-complete vim-X11 centos-release-dotnet git nuget wget mesa-dri-drivers xorg-x11-xauth xorg-x11-font-utils fontconfig code dotnet-sdk-2.1 msbuild
    curl -Lsfo /tmp/build-cake.sh https://cakebuild.net/download/bootstrapper/linux
    git clone --recursive https://github.com/phobos2390/tritanium-battles.git
    git clone --recursive https://github.com/phobos2390/MonopolySim.git
    git clone --recursive https://github.com/phobos2390/EuropanIndependence.git
    git clone --recursive https://github.com/cake-build/example.git

    code \
    --install-extension ms-vscode.csharp\
    --install-extension Leopotam.csharpfixformat\
    --install-extension jchannon.csharpextensions\
    --install-extension formulahendry.code-runner\
    --install-extension vscodevim.vim\
    --install-extension cake-build.cake-vscode\
    --install-extension jmrog.vscode-nuget-package-manager\
    --install-extension ms-vscode.mono-debug

    sudo yum install -y xorg-x11-fonts-Type1 urw-fonts dejavu-sans-fonts

  SHELL
end
