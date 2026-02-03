# Amazon Reviews Analysis

## Setup instructions

### Dataset

Download the dataset (*Amazon Reviews 2023 (c) McAuley Lab*) and place the unzipped files in the `data` directory.

- Reviews [mcauleylab.ucsd.edu](https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/review_categories/Books.jsonl.gz)

  - Mirror [huggingface.co](datasets/McAuley-Lab/Amazon-Reviews-2023/blob/main/raw/review_categories/Books.jsonl)
  
- Metadata [https://mcauleylab.ucsd.edu](https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/meta_categories/meta_Books.jsonl.gz)

  - Mirror [huggingface.co](https://huggingface.co/datasets/McAuley-Lab/Amazon-Reviews-2023/blob/main/raw/meta_categories/meta_Books.jsonl)


### Python environment

1. Create Python venv in the project root directory `python -m venv ./.venv`  

2. Activate the venv :
- Windows `.\.venv\Scripts\activate`
- Unix `source .venv/bin/activate`

3. Once in the venv, install the requirements `pip install -r requirements.txt`.

4.  Install Jupyter, either :
   - Via `pip install notebook` then open the notebook with `jupyter notebook main.ipynb`
   - Or via the [Jupyter extension in VSCode](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) if opened via VSCode. Then, "Run All Cells" in `main.ipynb`.


