# SilverStripe Queued Jobs CSV Export Module

## Maintainer Contact

Brett Tasker


## Requirements

* SilverStripe Queued Jobs Module 2.x

## Version info

The master branch of this module is currently aiming for SilverStripe 3.x compatibility

## Documentation

The Queued Jobs CSV Export module provides a process for downloading large CSV files using the SilverStripe Queued Jobs module. By default this job exports the SiteTree DataList.
This was designed to allow custom long running CSV exports to be pushed out to Queuejobs and be actioned via CLI to avoid any timeouts.

## Quick Usage Overview

* Extend the ExportObjectsCSVJob class and overwrite the functions as necessary.

```
class ExportJob extends ExportObjectsCSVJob {

    public function getTitle() {
        return 'Title of Export job';
    }

    protected function getDataList() {
        return DataList::create('MyMember')->where('"Age" > 14');
    }
    
    protected function getFields() {
        return array('GroupID', 'First name', 'Surname', 'Email');
    }

    /**
     * process per-line data to be exported to CSV
     * return Array
     */
    public function getExportData($object) {
 
        $data = array(
			$object->Group()->ID,
			$object->FirstName,
			$object->Surname,
			$object->Email
		)

        return $data;
    }
}
```

## Related

 * [silverstripe/gridfieldqueuedexport](https://github.com/silverstripe/silverstripe-gridfieldqueuedexport): Batched exports on GridField. Also uses queuedjobs, but provides a progress UI to the user.
