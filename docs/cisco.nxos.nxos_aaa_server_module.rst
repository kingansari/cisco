.. _cisco.nxos.nxos_aaa_server_module:


**************************
cisco.nxos.nxos_aaa_server
**************************

**Manages AAA server global configuration.**


Version added: 1.0.0

.. contents::
   :local:
   :depth: 1


Synopsis
--------
- Manages AAA server global configuration




Parameters
----------

.. raw:: html

    <table  border=0 cellpadding=0 class="documentation-table">
        <tr>
            <th colspan="1">Parameter</th>
            <th>Choices/<font color="blue">Defaults</font></th>
            <th width="100%">Comments</th>
        </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="parameter-"></div>
                    <b>deadtime</b>
                    <a class="ansibleOptionLink" href="#parameter-" title="Permalink to this option"></a>
                    <div style="font-size: small">
                        <span style="color: purple">string</span>
                    </div>
                </td>
                <td>
                </td>
                <td>
                        <div>Duration for which a non-reachable AAA server is skipped, in minutes or keyword &#x27;default. Range is 1-1440. Device default is 0.</div>
                </td>
            </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="parameter-"></div>
                    <b>directed_request</b>
                    <a class="ansibleOptionLink" href="#parameter-" title="Permalink to this option"></a>
                    <div style="font-size: small">
                        <span style="color: purple">string</span>
                    </div>
                </td>
                <td>
                        <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                    <li>enabled</li>
                                    <li>disabled</li>
                                    <li>default</li>
                        </ul>
                </td>
                <td>
                        <div>Enables direct authentication requests to AAA server or keyword &#x27;default&#x27; Device default is disabled.</div>
                </td>
            </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="parameter-"></div>
                    <b>encrypt_type</b>
                    <a class="ansibleOptionLink" href="#parameter-" title="Permalink to this option"></a>
                    <div style="font-size: small">
                        <span style="color: purple">string</span>
                    </div>
                </td>
                <td>
                        <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                    <li>0</li>
                                    <li>7</li>
                        </ul>
                </td>
                <td>
                        <div>The state of encryption applied to the entered global key. O clear text, 7 encrypted. Type-6 encryption is not supported.</div>
                </td>
            </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="parameter-"></div>
                    <b>global_key</b>
                    <a class="ansibleOptionLink" href="#parameter-" title="Permalink to this option"></a>
                    <div style="font-size: small">
                        <span style="color: purple">string</span>
                    </div>
                </td>
                <td>
                </td>
                <td>
                        <div>Global AAA shared secret or keyword &#x27;default&#x27;.</div>
                </td>
            </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="parameter-"></div>
                    <b>server_timeout</b>
                    <a class="ansibleOptionLink" href="#parameter-" title="Permalink to this option"></a>
                    <div style="font-size: small">
                        <span style="color: purple">string</span>
                    </div>
                </td>
                <td>
                </td>
                <td>
                        <div>Global AAA server timeout period, in seconds or keyword &#x27;default. Range is 1-60. Device default is 5.</div>
                </td>
            </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="parameter-"></div>
                    <b>server_type</b>
                    <a class="ansibleOptionLink" href="#parameter-" title="Permalink to this option"></a>
                    <div style="font-size: small">
                        <span style="color: purple">string</span>
                         / <span style="color: red">required</span>
                    </div>
                </td>
                <td>
                        <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                    <li>radius</li>
                                    <li>tacacs</li>
                        </ul>
                </td>
                <td>
                        <div>The server type is either radius or tacacs.</div>
                </td>
            </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="parameter-"></div>
                    <b>state</b>
                    <a class="ansibleOptionLink" href="#parameter-" title="Permalink to this option"></a>
                    <div style="font-size: small">
                        <span style="color: purple">string</span>
                    </div>
                </td>
                <td>
                        <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                    <li><div style="color: blue"><b>present</b>&nbsp;&larr;</div></li>
                                    <li>default</li>
                        </ul>
                </td>
                <td>
                        <div>Manage the state of the resource.</div>
                </td>
            </tr>
    </table>
    <br/>


Notes
-----

.. note::
   - Tested against NXOSv 7.3.(0)D1(1) on VIRL
   - Limited Support for Cisco MDS
   - The server_type parameter is always required.
   - If encrypt_type is not supplied, the global AAA server key will be stored as encrypted (type 7).
   - Changes to the global AAA server key with encrypt_type=0 are not idempotent.
   - state=default will set the supplied parameters to their default values. The parameters that you want to default must also be set to default. If global_key=default, the global key will be removed.
   - For information on using CLI and NX-API see the :ref:`NXOS Platform Options guide <nxos_platform_options>`
   - For more information on using Ansible to manage network devices see the :ref:`Ansible Network Guide <network_guide>`
   - For more information on using Ansible to manage Cisco devices see the `Cisco integration page <https://www.ansible.com/integrations/networks/cisco>`_.



Examples
--------

.. code-block:: yaml

    # Radius Server Basic settings
    - name: Radius Server Basic settings
      cisco.nxos.nxos_aaa_server:
        server_type: radius
        server_timeout: 9
        deadtime: 20
        directed_request: enabled

    # Tacacs Server Basic settings
    - name: Tacacs Server Basic settings
      cisco.nxos.nxos_aaa_server:
        server_type: tacacs
        server_timeout: 8
        deadtime: 19
        directed_request: disabled

    # Setting Global Key
    - name: AAA Server Global Key
      cisco.nxos.nxos_aaa_server:
        server_type: radius
        global_key: test_key



Return Values
-------------
Common return values are documented `here <https://docs.ansible.com/ansible/latest/reference_appendices/common_return_values.html#common-return-values>`_, the following are the fields unique to this module:

.. raw:: html

    <table border=0 cellpadding=0 class="documentation-table">
        <tr>
            <th colspan="1">Key</th>
            <th>Returned</th>
            <th width="100%">Description</th>
        </tr>
            <tr>
                <td colspan="1">
                    <div class="ansibleOptionAnchor" id="return-"></div>
                    <b>commands</b>
                    <a class="ansibleOptionLink" href="#return-" title="Permalink to this return value"></a>
                    <div style="font-size: small">
                      <span style="color: purple">list</span>
                    </div>
                </td>
                <td>always</td>
                <td>
                            <div>command sent to the device</div>
                    <br/>
                        <div style="font-size: smaller"><b>Sample:</b></div>
                        <div style="font-size: smaller; color: blue; word-wrap: break-word; word-break: break-all;">[&#x27;radius-server deadtime 22&#x27;, &#x27;radius-server timeout 11&#x27;, &#x27;radius-server directed-request&#x27;]</div>
                </td>
            </tr>
    </table>
    <br/><br/>


Status
------


Authors
~~~~~~~

- Jason Edelman (@jedelman8)
