# Canvas integration

Use the URLs in `colab_links.csv` as the targets of Canvas buttons or module links. A direct Colab link has this form:

```text
https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/notebooks/NB04_pairwise_alignment.ipynb
```

The `main` branch is the student-facing distribution branch. Develop and test on feature branches, then merge validated changes into `main`.

Each notebook contains the same permanent launch link at the top. To make a
Canvas button, replace `NOTEBOOK_ID` in this snippet with the exact filename
from `colab_links.csv` (without `.ipynb`):

```html
<p>
  <a href="https://colab.research.google.com/github/RobBurnap/Bioinformatics-MICR4203-MICR5203/blob/main/notebooks/NOTEBOOK_ID.ipynb"
     target="_blank" rel="noopener noreferrer">
    <img src="https://colab.research.google.com/assets/colab-badge.svg"
         alt="Open the assigned notebook in Google Colab">
  </a>
</p>
```

Recommended Canvas button label: **Open NBxx in Google Colab**.

Use `NB04_canvas_assignment.md` and `NB04_colab_button.html` as the completed
model. The other notebooks are launch-ready development shells; do not publish
their Canvas assignments until their guided analyses and starter data have
been completed and tested.

## Student launch sequence

1. Select the Canvas **Open in Colab** button.
2. In Colab, select **File → Save a copy in Drive**.
3. Keep the notebook identifier (`NB00`, `NB01`, and so forth) in the filename.
4. Run the notebook from top to bottom and approve Drive access when prompted.
5. Use the automatically selected course folder and the notebook-specific
   `Data/` and `Outputs/` folders.
