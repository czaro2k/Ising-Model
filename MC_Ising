import numpy as np
import matplotlib.pyplot as plt

def MC_Ising_model(beta, vis = False, N = 50, rng = 3000):
  s = np.random.choice([-1, 1],[N,N])
  numbers = np.arange(N*N).reshape(N,N)
  M_list = []
  blacks = ((numbers//N + numbers%N)%2).astype(bool)
  whites = np.logical_not(blacks)

  if vis == True:
    plt.rcParams['image.cmap'] = 'Wistia'
    fig, ax = plt.subplots(figsize=(16, 9))
    ax.imshow(s, vmin=0, vmax=1)
    ax.axis(False);

  for j in range(rng):
    m_i = np.roll(s, 1, axis=0)
    m_i += np.roll(s, -1, axis=0)
    m_i += np.roll(s, 1, axis=1)
    m_i += np.roll(s, -1, axis=1)

    p = 1/(1+np.exp(-2*beta*m_i))
    p = p.reshape(N,N)

    rand = np.random.random([N,N])
    up = np.where(p >= rand, True, False).reshape(N,N)

    steps = np.random.choice([0, 1],2)

    for i in steps:
      if i == 0:
        s[whites] = -1
        s[whites & up] = +1
      else:
        s[blacks] = -1
        s[blacks & up] = +1

    if j > rng/2:
      M = np.abs(np.mean(s))
      M_list.append(M)
      

  if vis == True:
    plt.rcParams['image.cmap'] = 'Wistia'
    fig, ax = plt.subplots(figsize=(16, 9))
    ax.imshow(s, vmin=0, vmax=1)
    ax.axis(False);
  
  M_mean = np.mean(M_list)
  chi = np.var(M_list)*beta

  M_list.clear()

  return M_mean, chi

betas = np.linspace(0.2,2,num=40)
print(betas)
data = []

for beta in betas:
  mb = []
  cb = []
  for i in range(10):
    values = (MC_Ising_model(beta))
    mb.append(values[0])
    cb.append(values[1])
  print(beta, np.mean(mb), np.mean(cb))  
  data.append([beta, np.mean(mb), np.mean(cb)])

data = np.array(data)
b = data[:,0]
m = data[:,1]
c = data[:,2]

plt.plot(b, m)
plt.show()
plt.plot(b, c)
plt.show()
