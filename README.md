# rabbitcj #

A rabbitmq client wrapper

# Install #

Install from source with `lein install` 


or add `:dependencies [[rabbitcj "0.1.0-SNAPSHOT"]]` to your
project.clj file

# Usage #

<pre><code>
(def c (connect {:username ""
                 :password ""
                 :virtual-host ""
                 :host ""
                 :port 1234}))

(def chan (create-channel c))

rabbitcj.client> (declare-exchange chan "messages" fanout-exchange true false nil)
#<DeclareOk #method<exchange.declare-ok>()>

rabbitcj.client> (declare-queue chan "message-q" true false false nil)
#<DeclareOk #method<queue.declare-ok>(queue=message-q,message-count=0,consumer-count=0)>

rabbitcj.client> (bind-queue chan "message-q" "messages" "")
#<BindOk #method<queue.bind-ok>()>

rabbitcj.client> (publish chan "messages" "" "hello, world!")
nil

rabbitcj.client> (def cns (consumer chan "message-q"))
#'rabbitcj.client/cns

rabbitcj.client> (consume chan cns 15)
"hello, world!"

<pre><code>