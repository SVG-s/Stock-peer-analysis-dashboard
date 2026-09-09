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

#################################################################################################
GitHub itself does not need requirements.txt. Your deployed Streamlit app needs it.

Think of it this way:

Git/GitHub = stores your project files and code.
Streamlit Cloud = takes those files and creates a new Python environment on its server.
requirements.txt = tells Streamlit Cloud which Python packages to install.
For example, your code says:

import yfinance as yf

Your computer already has yfinance because you ran:

pip install yfinance

But Streamlit Cloud is a different computer/environment. It doesn't automatically have your locally installed packages.

So when Streamlit Cloud sees:

import yfinance as yf

it needs to know:

"Which package do I install to make this import work?"

That's what this tells it:

yfinance==1.7.0

The flow is basically
Your computer
     │
     │ git push
     ▼
GitHub repository
     │
     │ Streamlit Cloud reads project
     ▼
Streamlit Cloud
     │
     │ reads requirements.txt
     ▼
installs yfinance
     │
     ▼
runs streamlit_app.py
     │
     ▼
🌐 Your public app

