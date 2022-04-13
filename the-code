import numpy as np


from pathlib import Path
import networkx as nx 
network_data = Path().cwd().parent / "data"
blogg = nx.read_graphml(network_data / "polblogs_directed.graphml")

print(nx.info(blogg))


network_data = Path().cwd().parent / "data"
blogg = nx.read_graphml(network_data / "polblogs_directed.graphml")

print(nx.info(blogg))


rd_nodes= list(nx.get_node_attributes(blogg, 'value').values())
num_nodes = len(blogg.nodes) 
num_nodes_dem = rd_nodes.count("1") 
num_nodes_rep = rd_nodes.count("0") 


values= nx.get_node_attributes(blogg, 'value')


d_sub=[]
r_sub=[]
for k,v in values.items():
    if v=="0":
        r_sub.append(k)
    else:
        d_sub.append(k)    
        
        
dem_sub= nx.subgraph(blogg,d_sub)
rep_sub= nx.subgraph(blogg,r_sub)

d_in_degree=0
for i,j in list(dem_sub.edges):
    if (i in list(dem_sub.nodes)) & (j in list(dem_sub.nodes)):
        d_in_degree+=1
#check: sum(list(dict(dem_sub.in_degree).values())) 

r_in_degree=0
for i,j in list(rep_sub.edges):
    if (i in list(rep_sub.nodes)) & (j in list(rep_sub.nodes)):
        r_in_degree+=1
#check: sum(list(dict(rep_sub.in_degree).values()))          
avg_degree_dem = d_in_degree/len(dem_sub.nodes) # ...
#check: np.mean(list(dict(dem_sub.in_degree).values()))
avg_degree_rep = r_in_degree/len(rep_sub.nodes) # ...
#check: np.mean(list(dict(rep_sub.in_degree).values()))
print(f"The average degree among the Democrats was {avg_degree_dem:0.2f}, whereas it was {avg_degree_rep:0.2f} among the Republicans.")


import matplotlib.pyplot as plt
G = nx.karate_club_graph()
attributes= [list(G.nodes[n].values())[0] for n in G.nodes]
labels=dict(enumerate(attributes))
colors = ['#1f78b4' if (n=='Mr. Hi') else '#9f91c9' for n in attributes]
plt.figure(1,figsize=(6,5))
nx.draw_networkx(G, pos=nx.spring_layout(G),node_color=colors,labels=labels)




import matplotlib.pyplot as plt 
import networkx as nx 

def make_connect_the_dots(g , pos, print_path=False):
    if (g == ...) or (pos ==...):
        print("Please run this again with a Graph object and a dictionary of positions.")
        return
    
    fig, (ax1, ax2) = plt.subplots(1,2)
    
    nx.draw_networkx_nodes(g,pos,
                           node_size=5,
                           ax=ax1)

    nx.draw_networkx_labels(g,pos,
                            font_size=5,
                            verticalalignment='bottom',
                            ax=ax1)

    nx.draw_networkx_nodes(g,pos,
                           node_size=10,
                           alpha=0.3,
                           ax=ax2)

    if list(g.nodes) != list(range(len(g.nodes))):
        print("The names of the nodes should be the integer numbers from 0 to n, where n is the last node.")
        return None
    
    edge_list = [(i, i+1) for i in range(len(g.nodes)-1)] + \
                [(len(g.nodes)-1,0)]
    
    g2 = g.copy()
    
    g2.add_edges_from(edge_list)
    
    nx.draw_networkx_edges(g2,pos,
                       edge_color="lightgrey",
                       ax=ax2)

    if print_path:
        extent = (ax1.get_window_extent()
        .transformed(fig.dpi_scale_trans.inverted()))
        fig.savefig(print_path, bbox_inches=extent)
    
    plt.show();


g=nx.Graph()
g.add_nodes_from(list(range(14)))

pos =  {0:(0,-12),
       1:(3.5,-6),2:(6.6,0),3:(7.7,3),4:(7,6.5),
       5:(5,8.2),6:(2.2,7.8),7:(0,6),8:(-2.2,7.8),9:(-5,8.2),10:(-7,6.5), 
    11:(-7.7,3),12:(-6.6,0),13:(-3.5,-6)}

make_connect_the_dots(g,pos, print_path="heart.pdf")




import requests
from pathlib import Path 
import networkx as nx 

data_folder = Path().cwd().parent / "data"

bison_g = nx.read_edgelist(data_folder / 
    "mammalia-bison-dominance/mammalia-bison-dominance.edges", 
                           data=(("num_interact",int),))

print(nx.info(bison_g))
print(bison_g.edges[('1', '2')])
print()

raccoon_g = nx.read_edgelist(data_folder / 
    "mammalia-raccoon-proximity/mammalia-raccoon-proximity.edges", 
                             data=(("var1",int),("var2",int)))

print(nx.info(raccoon_g))
print(raccoon_g.edges[('1', '2')])

attr_url = "https://raw.githubusercontent.com/bansallab/asnr/master/Networks/Mammalia/bats_roostuse_weighted/bat_silvis_roosting_attribute.graphml"
req = requests.get(attr_url)

with open("bat_silvis_roosting_attribute.graphml", "w") as f:
    f.write(req.text)

network_data = Path().cwd().parent / "Formatives"
batt = nx.read_graphml(network_data / "bat_silvis_roosting_attribute.graphml")
network_data = Path().cwd().parent / "data"/ "mammalia-bat-roosting-indiana.edges"
nx.read_weighted_edgelist(network_data, nodetype=int)
print(nx.info(batt))


plt.figure(1,figsize=(10,5))
plt.title("Figure 1")
node_sizes = [50*d for n,d in batt.degree()]
nx.draw_networkx(batt, pos=nx.spring_layout(batt),node_size=node_sizes,with_labels=False,alpha=0.15)


ages= nx.get_node_attributes(batt, 'Age (2009)')
adult_n=[k for k,v in ages.items() if (ages[k]=="adult")]
juv_n= [k for k,v in ages.items() if (ages[k]=="juv")]

colors = ['#1f78b1' if (n in adult_n) else '#9f91c9' for n in batt.nodes]

plt.figure(1,figsize=(10,5))
plt.title("Figure 2: Ages")
nx.draw_networkx(batt, pos=nx.spring_layout(batt,iterations=100),node_color=colors,with_labels=False,alpha=0.5)


#random edges and positions with center
import random
def rand_cent(node_n,central_n):
    nodes= list(range(node_n))
    cent= random.sample(nodes,central_n)
    edges=[]
    positions={}
    colors={}
    centre=[]
    for i in nodes:
        rest=nodes[:i]+nodes[i+1:]
        if i in cent:
            colors[i]='#9f91c9'
            positions[i]=(random.uniform(-.1,.4),random.uniform(0.540,0.549))
            for j in rest:
                if not (i,j) or not (j,i) in edges:
                    edges.append((i,j))
                if j in cent:
                    if not (i,j) or not (j,i) in centre:
                        centre.append((i,j))
                    
            
        else:
            colors[i]='#1f78b1'
            positions[i]=(random.uniform((-1.2),(.4)),random.uniform((0.560),(0.563)))
            for c in cent:
                if not (i,c) or not (c,i) in edges:
                    edges.append((i,c))                
    

    return cent,centre,colors,positions,edges
    
g_pos=nx.Graph()
edgelist = [('a','b'),('b','c'),('a','c'),('d','a'),('d','b'),('e','a'),('e','b'),('e','c'),('e','d')]
g_pos.add_edges_from(edgelist)
pos = { 'a':(.45,0.54),
    'b':(.30,0.54),
    'c':(-.1,0.538),
    'd':(0.95,0.537),
    'e':(0.37,0.5407)}

fig,axs= plt.subplots(1,4, figsize=(12, 4))
normed_degrees = {k:100*(v/sum(list(dict(g_pos.degree()).values()))) for k,v in dict(g_pos.degree()).items()}
node_sizes = [(d**2.6) for n,d in normed_degrees.items()]
#node_sizes = [(d**5.5) for n,d in g_pos.degree()]
nx.draw_networkx_nodes(g_pos,pos,alpha=0.3,node_size=node_sizes,ax=axs[0]) 
nx.draw_networkx_edges(g_pos,pos,ax=axs[0])
nx.draw_networkx_labels(g_pos,pos,ax=axs[0])

g_post=nx.Graph()
edgelist1 = [('a','b'),('b','c'),('a','c'),('d','a'),('d','b'),('e','a'),('e','b')]
g_post.add_edges_from(edgelist1)
pos = {'a':(.45,0.54),
    'b':(.30,0.54),
    'c':(-.1,0.538),
    'd':(0.95,0.537),
    'e':(0.90,0.541)}
normed_degrees = {k:100*(v/sum(list(dict(g_post.degree()).values()))) for k,v in dict(g_post.degree()).items()}
node_sizes = [(d**2.6) for n,d in normed_degrees.items()]
nx.draw_networkx_nodes(g_post,pos,alpha=0.3,node_size=node_sizes,ax=axs[1]) 
nx.draw_networkx_edges(g_post,pos,ax=axs[1])
nx.draw_networkx_labels(g_post,pos,ax=axs[1])

g_post=nx.Graph()
cent,centre,colors,positions,edges=rand_cent(10,5)
color=[v for k,v in colors.items()]

edges = [x for x in edges if x not in centre]
edgelist1 = edges
g_post.add_edges_from(edgelist1)
normed_degrees1 = {k:100*(v/sum(list(dict(g_post.degree()).values()))) for k,v in dict(g_post.degree()).items()}
pos = positions
node_sizes = [(d**3.5) for n,d in normed_degrees1.items()]
nx.draw_networkx_nodes(g_post,pos,alpha=0.5,node_size=node_sizes,ax=axs[2],node_color=color) 
nx.draw_networkx_edges(g_post,pos,ax=axs[2], edge_color = "lightgrey")
nx.draw_networkx_labels(g_post,pos,ax=axs[2])

g_post=nx.Graph()
cent,centre,colors,positions,edges=rand_cent(10,5)
color=[v for k,v in colors.items()]

edgelist1 = edges
g_post.add_edges_from(edgelist1)
normed_degrees1 = {k:100*(v/sum(list(dict(g_post.degree()).values()))) for k,v in dict(g_post.degree()).items()}

pos = positions
node_sizes = [(d**3.5) for n,d in normed_degrees1.items()]
nx.draw_networkx_nodes(g_post,pos,alpha=0.5,node_size=node_sizes,ax=axs[3],node_color=color) 
nx.draw_networkx_edges(g_post,pos,ax=axs[3], edge_color = "lightgrey")
nx.draw_networkx_labels(g_post,pos,ax=axs[3])
plt.tight_layout()

