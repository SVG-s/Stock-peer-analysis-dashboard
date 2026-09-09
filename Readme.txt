Recommended clean setup
I'd start fresh and create the environment in your project directory.

From PowerShell:

cd "C:\Users\User\PycharmProjects"

Create the environment:

& "C:\Program Files\Python313\python.exe" -m venv .venv

Activate it:

.\.venv\Scripts\Activate.ps1

Your prompt should then look something like:

(.venv) PS C:\Users\User\PycharmProjects>

Now install your packages inside the virtual environment:

python -m pip install --upgrade pip
python -m pip install streamlit yfinance

Check that you're using the correct Python:

python -c "import sys; print(sys.executable)"

It should show:

C:\Users\User\PycharmProjects\.venv\Scripts\python.exe

Then verify both packages:

python -c "import streamlit, yfinance; print('OK')"

You should get:

OK

Finally:

python -m streamlit run streamlit_app.py

This is preferable to simply streamlit run ... because it guarantees that Streamlit is launched by the same Python environment you're using.

