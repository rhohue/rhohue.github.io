{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "https://youtu.be/RrUTwq5jKM4\n",
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import qiskit"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "metadata": {},
   "outputs": [],
   "source": [
    "from qiskit import IBMQ"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "configrc.store_credentials:WARNING:2021-03-03 15:13:19,057: Credentials already present. Set overwrite=True to overwrite.\n"
     ]
    }
   ],
   "source": [
    "IBMQ.save_account('4bdc51e9e8030f7b0b091c56b6b0a158cfe98f3fbb8a5dffa44bc622d1370fd4caf3a903a7724d0794807cf999d8da452fa1b08e574ed808b804e69f04e3e842')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "from qiskit import *"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "qr=QuantumRegister(2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "cr=ClassicalRegister(2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "circuit=QuantumCircuit(qr, cr)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [],
   "source": [
    "%matplotlib inline"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<pre style=\"word-wrap: normal;white-space: pre;background: #fff0;line-height: 1.1;font-family: &quot;Courier New&quot;,Courier,monospace\">         \n",
       "q0_0: |0>\n",
       "         \n",
       "q0_1: |0>\n",
       "         \n",
       " c0: 0 2/\n",
       "         </pre>"
      ],
      "text/plain": [
       "         \n",
       "q0_0: |0>\n",
       "         \n",
       "q0_1: |0>\n",
       "         \n",
       " c0: 0 2/\n",
       "         "
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "circuit.draw(initial_state=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<qiskit.circuit.instructionset.InstructionSet at 0x17d3f720e20>"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "circuit.h(qr[0])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 159.633x204.68 with 1 Axes>"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "circuit.draw(output=\"mpl\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<qiskit.circuit.instructionset.InstructionSet at 0x17d40897ee0>"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "circuit.cx(qr[0],qr[1])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 263.676x204.68 with 1 Axes>"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "circuit.draw(initial_state=True,output=\"mpl\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<qiskit.circuit.instructionset.InstructionSet at 0x17d40928220>"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "circuit.measure(qr,cr)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 384.076x204.68 with 1 Axes>"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "circuit.draw(initial_state=True, output=\"mpl\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [],
   "source": [
    "simulator=Aer.get_backend('qasm_simulator')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<qiskit.providers.aer.aerjob.AerJob at 0x17d408ef8b0>"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "execute(circuit, backend=simulator)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [],
   "source": [
    "result=execute(circuit, backend=simulator).result()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [],
   "source": [
    "from qiskit.tools.visualization import plot_histogram"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAc0AAAE6CAYAAAB00gm8AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjIsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+WH4yJAAAgAElEQVR4nO3df5xWdZ338ddHJggXMcH4jQIKuECC0yhLEbhbZlm36+ruKmWtt6W32ertw9vdaqu7rbbsh/3QzCz2h62VWFp3bemuZguI0thAUkABuwwsjPwIpMUfiM74uf+4rqGLYRjOyMX84vV8PObBdX3P95zrcxwu3p5zvud7IjORJEmHdkx3FyBJUm9haEqSVJChKUlSQYamJEkFGZqSJBVkaEqSVFBNdxfQnU488cQcN25cd5chSepBli1btiMzX9nesqM6NMeNG0dDQ0N3lyFJ6kEiYuPBlnX56dmIuDoiGiPiuYhYFhGvO0T/iIjrIuLXEbE3IrZExKfa9Jlb3tZzEbE+Iq46snshSToadWloRsTFwM3AJ4EzgEeB+yPipA5W+xxwNfA+4PeB84DFFdscD9xX3tYZwI3AlyLioiOxD5Kko1d05TR6EVEP/CIzr6hoWwfck5kfaKf/ZGAlcHpm/uog2/w0cGFmTqxo+3tgambO6qieurq69PSsJKlSRCzLzLr2lnXZkWZE9AdeDTzQZtEDwGsOstofA+uBN5VPu26IiK9HxLCKPrPa2ea/AXUR8bIqlC5JEtC1A4FOBPoB29q0bwPecJB1JgAnA5cAlwEJ3AT8S0TMyswXgRHAj9vZZk35M7dULoiIK4ErAUaNGsXChQtLHzRhAscddxwrVqwAYOjQoUydOpXFi0tngmtqapg9ezbLly9n9+7dANTV1bFt2zY2bdoEwMSJExkwYAArV64EYNiwYUyaNIklS5YAMGDAAGbNmkVDQwNPP/00ADNnzmTz5s00NTUBMHnyZPr168fq1asBGDFiBOPHj2fp0qUADBw4kJkzZ1JfX8+ePXsAmDVrFo2NjWzduhWAKVOm0NLSwpo1awAYPXo0Y8aMob6+HoBBgwZRV1fH0qVL2bt3LwCzZ89m7dq1bN++HYBp06axd+9e1q1bB8DYsWMZPnz4voFTgwcPpra2liVLltDc3AzAnDlzWLVqFTt37gRg+vTpPPXUU6xfvx4oDbwaMmQIy5cvB+CEE05g+vTpLFq0iMwkIpg7dy4rVqxg165dANTW1vLkk0+yYcMGf0/+nvw9+Xvqkt9TR7rs9GxEjAKagDmZ+XBF+0eAeZl5WjvrfA24ApicmWvLbZOANcAfZGZ9RKwF7szMj1esNxdYCIzMzK0Hq8nTs5KktnrE6VlgB9BC6ciw0jAOPPpstQVobg3MsnVAM9A6eGjrQbbZDOw8nIIlSarUZaGZmc8Dy4Bz2iw6h9LI1/Y8AtRExCkVbRMonXptvY9mKQee3j0HaMjMFw6raEmSKnT1fZqfBy6LiHdHxO9HxM3AKOB2gIi4MSIequj/Y2A58I8RcUZEnAH8I1APtJ5XvR0YExFfLG/z3ZSuf97UNbskSTpadOmMQJl5d0QMBT4EjKR0O8l5mdl61DgSOKWi/4sR8VbgFkr3Zu4BHgSuLw8CIjMbI+I84AvAe4AngGsz894u2i1J0lGiS+/T7GkcCCRJaqunDASSJKlXMzQlSSrI0JQkqSBDU5KkggxNSZIKMjQlSSrI0JQkqSBDU5KkggxNSZIKMjQlSSrI0JQkqSBD8yj3r//6r0yePJlTTz2VT33qUwcsX7hwIccffzwzZsxgxowZfOxjH9u37PLLL2fYsGFMmzZtv3U+/OEPc/rppzNjxgze+MY38sQTTxzx/ZCkruCE7UfxhO0tLS1MmjSJBx98kDFjxnDmmWdy1113MWXKlH19Fi5cyE033cQPf/jDA9ZfvHgxgwYN4p3vfCcrV67c1757924GDx4MwC233MLq1au5/fbbj/wOSVIVOGG72vXYY49x6qmnMmHCBPr3788ll1zC97///cLrz5kzhyFDhhzQ3hqYAM888wwRUZV6Jam7GZpHsaamJsaOHbvv/ZgxY2hqajqg39KlS5k+fTpvfvObWbVqVaFtf/CDH2Ts2LF885vf3O+UriT1ZobmUay9U/Ntjwpra2vZuHEjK1as4JprruGCCy4otO1PfOITbNq0ibe//e3ceuutValXkrqboXkUGzNmDJs2bdr3fvPmzYwaNWq/PoMHD2bQoEEAnHfeebzwwgvs2LGj8Ge87W1v4957761OwZLUzQzNo9iZZ57JunXraGxs5Pnnn2fBggWcf/75+/XZunXrviPSxx57jBdffJGhQ4d2uN1169bte/2DH/yA0047rfrFS1I3qOnuAtR9ampquPXWWzn33HNpaWnh8ssvZ+rUqftGul511VXcc889fOUrX6GmpoaBAweyYMGCfadw582bx8KFC9mxYwdjxozhox/9KO9617t4//vfz5o1azjmmGM4+eSTHTkrqc/wlpOj+JYTSdKBvOVEkqQqMDQlSSrI0JQkqSBDU5J6iUPNFd3qZz/7Gf369eOee+7Z1/aFL3yBqVOnMm3aNObNm8dzzz0HwMUXX7xvbulx48YxY8aMI74fvZmhKUm9QEtLC+9973u5//77Wb16NXfddRerV69ut9/73vc+zj333H1tTU1N3HLLLTQ0NLBy5UpaWlpYsGABAHfffTePP/44jz/+OBdddBEXXnhhl+1Tb2RoSlIvUHSu6C996UtcdNFFDBs2bL/25uZm9uzZQ3NzM88+++wBE5lkJt/+9reZN2/eEd2P3s7QlKReoMhc0U1NTXzve9/jqquu2q999OjR3HDDDZx00kmMHDmS448/nje+8Y379Xn44YcZPnw4EydOPHI70QcYmpLUCxSZK/q6667j05/+NP369duvfdeuXXz/+9+nsbGRJ554gmeeeYZvfOMb+/W56667PMoswBmBJKkXKDJXdENDA5dccgkAO3bs4L777qOmpoYXXniB8ePH88pXvhKACy+8kEcffZRLL70UKJ26/e53v8uyZcu6aG96L0NTknqByrmiR48ezYIFC/jWt761X5/GxsZ9ry+77DLe+ta3csEFF1BfX89Pf/pTnn32WQYOHMhDDz1EXd3vJrz58Y9/zGmnncaYMWO6bH96K0NTknqBInNFH8zMmTP50z/9U2pra6mpqeGMM87gyiuv3Ld8wYIFnpotyLlnnXtWklSho7lnPdKsgiu+2N0V6EiYf113VyCpp3H0rCRJBRmakiQVZGhKklSQoSlJUkGGpiRJBRmakiQVZGhKklSQoSlJUkGGpiRJBRmakiQV5DR6ko46Tn3ZN3XF1JceaUqSVJChKUlSQYamJEkFGZqSJBVkaEqSVJChKUlSQYamJEkFGZqSJBVkaEqSVJChKUlSQYamJEkFGZqSJBXU5aEZEVdHRGNEPBcRyyLidQXXmxgRT0XE023az46IbOfntCOzB5Kko1WXhmZEXAzcDHwSOAN4FLg/Ik46xHr9gQXA4g66TQVGVvysq0bNkiS16uojzeuBOzJz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\n",
      "text/plain": [
       "<Figure size 504x360 with 1 Axes>"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "plot_histogram(result.get_counts(circuit))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "ibmqfactory.load_account:WARNING:2021-03-03 15:42:36,901: Credentials are already in use. The existing account in the session will be replaced.\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "<AccountProvider for IBMQ(hub='ibm-q', group='open', project='main')>"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "IBMQ.load_account()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [],
   "source": [
    "provider = IBMQ.get_provider('ibm-q')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [],
   "source": [
    "qcomp = provider.get_backend('ibmq_16_melbourne')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [],
   "source": [
    "job = execute(circuit, backend=qcomp)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [],
   "source": [
    "from qiskit.tools.monitor import job_monitor"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Job Status: job has successfully run\n"
     ]
    }
   ],
   "source": [
    "job_monitor(job)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [],
   "source": [
    "result=job.result()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 504x360 with 1 Axes>"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "plot_histogram(result.get_counts(circuit))"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
