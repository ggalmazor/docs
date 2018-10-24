Using ODK Briefcase
======================

.. _pull-from-aggregate:

Pulling forms from Aggregate
----------------------------

Cocotero

To download blank forms and completed form instances from an :doc:`Aggregate <aggregate-intro>` server:

#. Open the :guilabel:`Pull` tab.
#. Select *Aggregate server* in the :guilabel:`Pull from` drop-down.
#. Click the :guilabel:`Configure` button.
#. Enter the URL and login credentials for your Aggregate server in the dialog that pops up and click the :guilabel:`Connect` button.

   If you have anonymous login enabled on Aggregate, no login credentials are needed here.
   
   To connect to the `Aggregate Demo Server`_, the URL is https://opendatakit.appspot.com.
   
   .. _Aggregate Demo Server: https://opendatakit.appspot.com

#. Briefcase will show a list of forms for download. Only forms that are marked in Aggregate as downloadable will be shown.

#. Select the forms you want to download and click :guilabel:`Pull`. The selected forms will be pulled to your :ref:`Briefcase Storage <briefcase_storage>` location.

   For each selected form, Briefcase will pull down:
   
   - The form definition file (that is, the blank XForm).
   - All media associated with the form.
   - Completed form instances, including all their attached media files.

   If you have previously pulled the form:
   
   - The form definition file and media files will not be pulled.
   - New instances will be downloaded.

   .. warning::

     If your local copy and the remote copy of the blank form definition file are different, the pull will be aborted.

     .. rubric:: Workaround
     
     If the form definition has changed, but the changes only affect the question text and do not alter the structure of the collected data (or change the form ID or version), you can:
     
     #. In :guilabel:`Settings`, temporarily change the :ref:`Briefcase Storage <briefcase_storage>` location.
     #. Pull data into to the new location.
     #. Manually copy the instances from the temporary location of your original storage location.
     #. Update :guilabel:`Settings` back to the original :ref:`Briefcase Storage <briefcase_storage>` location.

.. note::
  :name: briefcase-parallel-connections

  .. rubric:: Pull forms faster with parallel connections
  
  .. container:: details
  
    To speed up pulling forms from Aggregate, enable :guilabel:`Pull submissions in parallel` in the :guilabel:`Settings` tab.

    .. image:: /img/briefcase-using/pull-in-parallel.*

    However, if your Aggregate server is :doc:`installed on Google App Engine <aggregate-app-engine>`, this setting may cause problems with large attachments. If your form has submission attachments (file uploads, videos, images, sound recordings) you should experiment with this setting and see if it improves or worsens performance.

.. _pull-from-collect:

Pulling forms from Collect
------------------------------

#. Ensure all filled-in forms are finalized.

   If you have incomplete forms that you cannot finalize before pulling into Briefcase, delete them. If you need to keep them, make a copy of :file:`/sdcard/odk` before deleting them, and restore it after you are finished.

#. Create a zip archive of the entire :file:`odk` directory.

   .. tip::

     You'll need to use an app for this.

     One option is `OI File Manager <https://play.google.com/store/apps/details?id=org.openintents.filemanager>`_.

#. Connect your Android device to your computer using a USB cable and choose to mount it as a Media device.
#. Copy the zip file you created from the Android device to your local hard drive.
#. Once it is copied onto your local hard drive, unzip the file.
#. In Briefcase, open the :guilabel:`Pull` tab.
#. Select *Collect directory* in the :guilabel:`Pull from` drop-down.
#. Click the :guilabel:`Configure` button and select the unzipped :file:`odk` folder.
#. Select the forms you want to download and click :guilabel:`Pull`. The selected forms will be pulled to your :ref:`Briefcase Storage <briefcase_storage>` location.
#. On the Android device, open Collect and delete the filled-in forms.

   .. tip::

     - You can use the *Collect directory* any time you want to pull forms from custom location.
     - You can confirm that the forms have been successfully pulled into Briefcase by confirming a successful pull status or by verifying the data appearing in a :ref:`CSV export file <briefcase-export-to-csv>`.

.. warning::

  Briefcase cannot discriminate between duplicate form instances. After you pull completed forms into Briefcase, it is important that you delete them from Collect. Otherwise, the next time you pull in forms, you will create duplicates.

.. note::

  Briefcase does not support pushing blank forms to Collect. Instead, :ref:`manually load the forms on your Collect device <loading-forms-directly>`.

.. _pull-form-definition:

Pulling form definitions
------------------------

#. Open the :guilabel:`Pull` tab.
#. Select *Form definition* in the :guilabel:`Pull from` drop-down.
#. Click the :guilabel:`Configure` button and select the :file:`.xml` form definition file.
#. Select the form and click :guilabel:`Pull`. The form will be pulled to your :ref:`Briefcase Storage <briefcase_storage>` location.

.. tip::

  This enables a workflow to upload forms with media attachments to Aggregate:

  #. Pull the form using the :guilabel:`Pull from` option.
  #. :ref:`Push the form to your Aggregate server <push-to-aggregate>`.

.. warning::

  Ensure that all attached media is available relative to the form definition file location.

.. _push-to-aggregate:

Pushing forms to Aggregate
--------------------------

To upload blank forms and completed form instances to an :doc:`Aggregate <aggregate-intro>` server:

#. Open the :guilabel:`Push` tab.
#. Select *Aggregate server* in the :guilabel:`Push to` drop-down.
#. Click the :guilabel:`Configure` button.
#. Enter the URL and login credentials for your Aggregate server in the dialog that pops up and click the :guilabel:`Connect` button.

   If you have anonymous login enabled on Aggregate, no login credentials are needed here.
   
   To connect to the `Aggregate Demo Server`_, the URL is https://opendatakit.appspot.com.
   
   .. _Aggregate Demo Server: https://opendatakit.appspot.com

#. Select the forms you want to upload and click :guilabel:`Push`. The selected forms will be pushed from your :ref:`Briefcase Storage <briefcase_storage>` to the Aggregate server.

   For each selected form, Briefcase will upload:

     - The form definition file (that is, the blank XForm).
     - All media associated with the form.
   
   - Completed form instances, including all their attached media files.

   .. warning::

     If your local copy and the remote copy of the blank form definition file are different, the push will be aborted.
   
     .. rubric:: Workaround
     
     If the form definition has changed, but the changes only affect the question text and do not alter the structure of the collected data (or change the form ID or version), you can:
     
     #. In :guilabel:`Settings`, temporarily change the :ref:`Briefcase Storage <briefcase_storage>` location.
     #. Manually copy the form directory from your original storage location of the temporary location.
     #. Replace the local form definition file with a copy of the version from your Aggregate server.
     #. Push your form instances. 
     #. Update :guilabel:`Settings` back to the original :ref:`Briefcase Storage <briefcase_storage>` location.

.. _briefcase-export-to-csv:

Export forms to CSV
-------------------

#. Open the :guilabel:`Export` tab.
#. Click on the :guilabel:`Set Default Configuration` button.

  - Set an :guilabel:`Export directory`.
  - If exporting :doc:`encrypted-forms`, set the corresponding :guilabel:`PEM file location`. See :ref:`the Encrypted forms section <create-key>` for more information.
  - If you wish, select a :guilabel:`Start date` and an :guilabel:`End date` to specify a limited date range to export.
  - Toggle export parameters as needed:

    - :guilabel:`Export media files` enables exporting media files into the chosen export directory
    - :guilabel:`Overwrite existing files` enables overwriting form instance data in the output files. The default behavior is to append data.
    - :guilabel:`Split select multiples` enables splitting select multiple fields. Enabling this setting will create an extra output column per select choice, with a `1` if the choice was selected, or `0` otherwise. This only affects select fields without a choice filter and that are not from an external file.
    - :guilabel:`Pull before export` enables trying to pull the selected forms in case there are new form instances to be exported.

#. Select the forms to export.

   If you are selecting and exporting more than one form, you may need to set individual export settings. To do this, click the gear icon (:guilabel:`⚙`) next to the form name.
   
#. Click :guilabel:`Export`.

.. _cli-use:

Working with the command line
-----------------------------

Briefcase has a command line interface (CLI) to enable scripting of many of the actions that can be taken in the graphical user interface (GUI).

.. versionadded:: 1.4.4
  A CLI was added.

.. versionadded:: 1.9.0
  The CLI first takes an operation parameter and then modifiers to that operation

.. _briefcase-cli-help:

Getting CLI help
~~~~~~~~~~~~~~~~

To get help about the command line operation:

.. code-block:: console

  $ java -jar {path/to/briefcase-jar-file} --help

.. _pull-from-aggregate-cli:
  
Pulling forms from Aggregate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- CLI flag: `-plla` or `--pull_aggregate`
- Usage:

  .. code-block:: console

      $ java -jar {path/to/briefcase-jar-file} --pull_aggregate --form_id {form-id} --storage_directory {path/to/briefcase-storage-location} --aggregate_url {aggregate-url} --odk_username {username} --odk_password {password}

- Help section:

  .. code-block:: none

      Params for -plla operation:
        -id,--form_id <arg>                 Form ID
        -p,--odk_password <arg>             ODK Password
        -sd,--storage_directory <arg>       Briefcase storage directory
        -u,--odk_username <arg>             ODK Username
        -url,--aggregate_url <arg>          Aggregate server URL
      Optional params for -plla operation:
        -pp,--parallel_pull                 Pull submissions in parallel

.. _pull-from-collect-cli:
  
Pulling forms from Collect
~~~~~~~~~~~~~~~~~~~~~~~~~~

This command assumes you have already copied and unzipped the :file:`odk` file :ref:`as described here <pull-from-collect>`.

- CLI flag: `-pc` or `--pull_collect`
- Usage:

  .. code-block:: console

      $ java -jar {path/to/briefcase-jar-file} --pull_collect --storage_directory {path/to/briefcase-storage-location} --odk_directory {path/to/unzipped-odk-file}

- Help section:

  .. code-block:: none

      Params for -pc operation:
        -od,--odk_directory <arg>           ODK directory
        -sd,--storage_directory <arg>       Briefcase storage directory
      Optional params for -pc operation:
        -id,--form_id <arg>                 Form ID

.. warning::

  This CLI operation **will pull all forms** present on the :file:`odk` directory if no `-id` parameter is defined.

.. _push-to-aggregate-cli:

Pushing forms to Aggregate
~~~~~~~~~~~~~~~~~~~~~~~~~~

- CLI flag: `-psha` or `--push_aggregate`
- Usage:

  .. code-block:: console

      $ java -jar {path/to/briefcase-jar-file} --push_aggregate --form_id {form-id} --storage_directory {path/to/briefcase-storage-location} --aggregate_url {aggregate-url} --odk_username {username} --odk_password {password}

- Help section:

  .. code-block:: none

      Params for -psha operation:
        -id,--form_id <arg>                 Form ID
        -p,--odk_password <arg>             ODK Password
        -sd,--storage_directory <arg>       Briefcase storage directory
        -u,--odk_username <arg>             ODK Username
        -url,--aggregate_url <arg>          Aggregate server URL
      Optional params for -psha operation:
        -fsb,--force_send_blank             Force sending the blank form to the Aggregate instance

.. warning::

  This CLI operation will only update the blank form if it does not already exist, whereas the GUI will always update the form.

.. _export-to-csv-cli:
  
Exporting forms to CSV
~~~~~~~~~~~~~~~~~~~~~~

- CLI flag: `-e` or `--export`
- Usage:

  .. code-block:: console

    $ java -jar {path/to/briefcase-jar-file} --export --form_id {form-id} --storage_directory {path/to/briefcase-storage-location} --export_directory {path/to/output-directory} --export_filename {output-file-name.csv}

- Help section:

  .. code-block:: none

      Params for -e operation:
        -ed,--export_directory <arg>        Export directory
        -f,--export_filename <arg>          Filename for export operation
        -id,--form_id <arg>                 Form ID
        -sd,--storage_directory <arg>       Briefcase storage directory
      Optional params for -e operation:
        -em,--exclude_media_export          Exclude media in export
        -end,--export_end_date <arg>        Export end date (inclusive) (yyyy-MM-dd or yyyy/MM/dd)
        -oc,--overwrite_csv_export          Overwrite files during export
        -pb,--pull_before                   Pull before export
        -pf,--pem_file <arg>                PEM file for form decryption
        -ssm,--split_select_multiples       Split select multiple fields
        -start,--export_start_date <arg>    Export start date (inclusive) (yyyy-MM-dd or yyyy/MM/dd)

.. _clear-saved-preferences:

Clear saved preferences
~~~~~~~~~~~~~~~~~~~~~~~

- CLI flag: `-c` or `--clear_prefs`
- Usage:

  .. code-block:: console

    $ java -jar {path/to/briefcase-jar-file} --clear_prefs
