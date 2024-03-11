### Ayugram desktop flake

#### To install, add this to your flake:

```nix
inputs = {
  ayugram-desktop.url = "github:shwewo/ayugram-desktop";
  # your other flakes...
};
```

To use my binary cache, add this to nix config:

```nix
nix = {
  settings = {
    substituters = [
      "https://shwewo.cachix.org"
    ];
    trusted-public-keys = [
      "shwewo.cachix.org-1:84cIX7ETlqQwAWHBnd51cD4BeUVXCyGbFdtp+vLxKOo="
    ];
    # other options...
  };
};
```

To use it in your system add this to your configuration.nix: 

```nix
environment.systemPackages = with pkgs; [
  inputs.ayugram-desktop.packages.${pkgs.system}.default
];
```

Also don't forget to add `inherit inputs` to your `flake.nix` like that:

```nix
nixosConfigurations.hostname = nixpkgs.lib.nixosSystem {
  system = "x86_64-linux";
  specialArgs = { 
    inherit inputs;   
  };

  # other configuration...
}
```