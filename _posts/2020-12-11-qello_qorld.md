#!/usr/bin/env python
# coding: utf-8

# https://youtu.be/RrUTwq5jKM4


# In[1]:


import qiskit


# In[38]:


from qiskit import IBMQ


# In[4]:


IBMQ.save_account('4bdc51e9e8030f7b0b091c56b6b0a158cfe98f3fbb8a5dffa44bc622d1370fd4caf3a903a7724d0794807cf999d8da452fa1b08e574ed808b804e69f04e3e842')


# In[1]:


from qiskit import *


# In[2]:


qr=QuantumRegister(2)


# In[3]:


cr=ClassicalRegister(2)


# In[4]:


circuit=QuantumCircuit(qr, cr)


# In[5]:


get_ipython().run_line_magic('matplotlib', 'inline')


# In[6]:


circuit.draw(initial_state=True)


# In[7]:


circuit.h(qr[0])


# In[8]:


circuit.draw(output="mpl")


# In[9]:


circuit.cx(qr[0],qr[1])


# In[10]:


circuit.draw(initial_state=True,output="mpl")


# In[11]:


circuit.measure(qr,cr)


# In[12]:


circuit.draw(initial_state=True, output="mpl")


# In[15]:


simulator=Aer.get_backend('qasm_simulator')


# In[17]:


execute(circuit, backend=simulator)


# In[18]:


result=execute(circuit, backend=simulator).result()


# In[20]:


from qiskit.tools.visualization import plot_histogram


# In[21]:


plot_histogram(result.get_counts(circuit))


# In[23]:


IBMQ.load_account()


# In[26]:


provider = IBMQ.get_provider('ibm-q')


# In[27]:


qcomp = provider.get_backend('ibmq_16_melbourne')


# In[28]:


job = execute(circuit, backend=qcomp)


# In[29]:


from qiskit.tools.monitor import job_monitor


# In[32]:


job_monitor(job)


# In[33]:


result=job.result()


# In[34]:


plot_histogram(result.get_counts(circuit))

