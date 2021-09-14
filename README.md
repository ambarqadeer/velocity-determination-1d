# velocity-determination-1d
Detection and 1d velocity determination of asteroids JWST MIRI imager data


* This repo is only for the 1dim motion simulation

EXECUTION STEPS:

    Code execution steps: (assuming mirisim has been installed and setup, assuming jwst pipeline has been installed)
    Duplicate the directory on git :
    Activate mirisim env and run the siulation file 'simulation.ini'
    Exit mirisim env, go back to base or env containing jwst pipeline and other libraries imported in cell 1 of velocity-determination.ipynb
    Update the' velocity-determination.ipynb' notebook

        correct ippath (directory of outpit from mirisim) and 'ipname' (indicating the exact output to use) in cell2 based on mirisim output you want to use
        In cell 4, update maskrefpath to a relevant refmask for the mirifov in your local miri crds, our simulations use ' … /crds/references/jwst/miri/jwst_miri_mask_0023.fits' and the 'do not use' flagged pixels where bit 0 is set are all filled with nan values



PLEASE NOTE :

Changes to stella's files before use for simulation -


Change_pixeldq.py :

    packaged in a function to accept two arguments, 1- input file path 2- output file path
    closed the open hdul at the end


function_move_source.py :

    added argument refmask which is the reference mask for the miri fov stacked to be the same size as the simulated science array from mirisim


move_source_code.py :

    packaged the execution part of the code into a function that accepts arguments move(inputdir, outputdir, velin, refmask, stattomoving = True):

    Velin is the multiple of 0.010996 arcsec/sec to be used for the simulation

    flag_move_source passed through the stattomoving argument and flipped, True now means move a stationary source

    Accepts and propagates the refmask array to function_move_source

    Closed the open hdul at the end

simulation files

    Point.ini : cen changed to '0 6' to ensure no artefacts exist close to our object row/column

    simulation.ini updated to change the name of the scene.ini file to point.ini


Except the addition of the refmask and correcting the scene file name, other changes do not improve the code in any way, but were intended to make it easier to use for our specific implementation
