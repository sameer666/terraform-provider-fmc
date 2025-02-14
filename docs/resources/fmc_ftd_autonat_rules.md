---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "fmc_ftd_autonat_rules Resource - fmc-terraform"
subcategory: ""
description: |-
  Resource for Auto NAT Rules in FMC
  Example
  An example is shown below:
  ```hcl
  resource "fmcftdautonatrules" "newrule" {
      natpolicy = fmcftdnatpolicies.natpolicy.id
      description = "Testing Auto NAT priv-pub"
      nattype = "static"
      sourceinterface {
          id = data.fmcsecurityzones.inside.id
          type = data.fmcsecurityzones.inside.type
      }
      destinationinterface {
          id = data.fmcsecurityzones.outside.id
          type = data.fmcsecurityzones.outside.type
      }
      originalnetwork {
          id = data.fmcnetworkobjects.private.id
          type = data.fmcnetworkobjects.private.type
      }
      translatednetwork {
          id = data.fmcnetworkobjects.public.id
          type = data.fmcnetworkobjects.public.type
      }
      translatednetworkisdestinationinterface = false
      originalport {
          port = 53
          protocol = "udp"
      }
      translatedport = 5353
      ipv6 = true
  }
  resource "fmcftdautonatrules" "newrule2" {
      natpolicy = fmcftdnatpolicies.natpolicy.id
      description = "Testing Auto NAT pub-priv"
      nattype = "dynamic"
      sourceinterface {
          id = data.fmcsecurityzones.inside.id
          type = data.fmcsecurityzones.inside.type
      }
      destinationinterface {
          id = data.fmcsecurityzones.outside.id
          type = data.fmcsecurityzones.outside.type
      }
      originalnetwork {
          id = data.fmchostobjects.CUCMPub.id
          type = data.fmchostobjects.CUCMPub.type
      }
      translatednetworkisdestinationinterface = false
      patoptions {
          patpooladdress {
              id = data.fmcnetworkobjects.private.id
              type = data.fmcnetworkobjects.private.type
          }
          extendedpattable = true
          roundrobin = true
      }
      ipv6 = true
  }
  ``
  **Note** If creating multiple rules during a singleterraform apply, remember to usedepends_on` to chain the rules so that terraform creates it in the same order that you intended.
---

# fmc_ftd_autonat_rules (Resource)

Resource for Auto NAT Rules in FMC

## Example
An example is shown below: 
```hcl
resource "fmc_ftd_autonat_rules" "new_rule" {
    nat_policy = fmc_ftd_nat_policies.nat_policy.id
    description = "Testing Auto NAT priv-pub"
    nat_type = "static"
    source_interface {
        id = data.fmc_security_zones.inside.id
        type = data.fmc_security_zones.inside.type
    }
    destination_interface {
        id = data.fmc_security_zones.outside.id
        type = data.fmc_security_zones.outside.type
    }
    original_network {
        id = data.fmc_network_objects.private.id
        type = data.fmc_network_objects.private.type
    }
    translated_network {
        id = data.fmc_network_objects.public.id
        type = data.fmc_network_objects.public.type
    }
    translated_network_is_destination_interface = false
    original_port {
        port = 53
        protocol = "udp"
    }
    translated_port = 5353
    ipv6 = true
}

resource "fmc_ftd_autonat_rules" "new_rule_2" {
    nat_policy = fmc_ftd_nat_policies.nat_policy.id
    description = "Testing Auto NAT pub-priv"
    nat_type = "dynamic"
    source_interface {
        id = data.fmc_security_zones.inside.id
        type = data.fmc_security_zones.inside.type
    }
    destination_interface {
        id = data.fmc_security_zones.outside.id
        type = data.fmc_security_zones.outside.type
    }
    original_network {
        id = data.fmc_host_objects.CUCMPub.id
        type = data.fmc_host_objects.CUCMPub.type
    }
    translated_network_is_destination_interface = false
    pat_options {
        pat_pool_address {
            id = data.fmc_network_objects.private.id
            type = data.fmc_network_objects.private.type
        }
        extended_pat_table = true
        round_robin = true
    }
    ipv6 = true
}
```
**Note** If creating multiple rules during a single `terraform apply`, remember to use `depends_on` to chain the rules so that terraform creates it in the same order that you intended.



<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **nat_policy** (String) The ID of the NAT policy this resource belongs to
- **nat_type** (String) The type of this resource, "static" or "dynamic"

### Optional

- **description** (String) The description of this resource
- **destination_interface** (Block List, Max: 1) Destination interface of this resource (see [below for nested schema](#nestedblock--destination_interface))
- **fallthrough** (Boolean) Enable Fallthrough
- **id** (String) The ID of this resource.
- **ipv6** (Boolean) Enable IPv6
- **net_to_net** (Boolean) Enable Net to Net
- **no_proxy_arp** (Boolean) Disable Proxy ARP
- **original_network** (Block List, Max: 1) Original network for this resource (see [below for nested schema](#nestedblock--original_network))
- **original_port** (Block List, Max: 1) Original port for this resource (see [below for nested schema](#nestedblock--original_port))
- **pat_options** (Block List, Max: 1) PAT options for this resource (see [below for nested schema](#nestedblock--pat_options))
- **perform_route_lookup** (Boolean) Enable perform route lookups for this resource
- **source_interface** (Block List, Max: 1) Source interface for this resource (see [below for nested schema](#nestedblock--source_interface))
- **translate_dns** (Boolean) Enable Translate DNS
- **translated_network** (Block List, Max: 1) Translated interface for this resource (see [below for nested schema](#nestedblock--translated_network))
- **translated_network_is_destination_interface** (Boolean) Interface is the destination translated network
- **translated_port** (Number) Translated port for this resource

### Read-Only

- **type** (String) The type of this resource

<a id="nestedblock--destination_interface"></a>
### Nested Schema for `destination_interface`

Required:

- **id** (String) The ID of this resource
- **type** (String) The type of this resource


<a id="nestedblock--original_network"></a>
### Nested Schema for `original_network`

Required:

- **id** (String) The ID of this resource
- **type** (String) The type of this resource


<a id="nestedblock--original_port"></a>
### Nested Schema for `original_port`

Required:

- **port** (Number)
- **protocol** (String)


<a id="nestedblock--pat_options"></a>
### Nested Schema for `pat_options`

Optional:

- **extended_pat_table** (Boolean) Enable Extended PAT table
- **include_reserve_ports** (Boolean) Include Reserve ports
- **interface_pat** (Boolean) Enable interface PAT
- **pat_pool_address** (Block List, Max: 1) Network Pool for PAT (see [below for nested schema](#nestedblock--pat_options--pat_pool_address))
- **round_robin** (Boolean) Enable Round Robin

<a id="nestedblock--pat_options--pat_pool_address"></a>
### Nested Schema for `pat_options.pat_pool_address`

Required:

- **id** (String) The ID of this resource
- **type** (String) The type of this resource



<a id="nestedblock--source_interface"></a>
### Nested Schema for `source_interface`

Required:

- **id** (String) The ID of this resource
- **type** (String) The type of this resource


<a id="nestedblock--translated_network"></a>
### Nested Schema for `translated_network`

Required:

- **id** (String) The ID of this resource
- **type** (String) The type of this resource


