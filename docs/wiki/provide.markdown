provide
=======

  While defining contracts local to the constrained function is nice
  (see [defconstrainedfn] for more information), very often you will find
  yourself in possession of an existing function that is not
  constrained:
  <div class="gist">
       <div class="gist-file">
          <div class="gist-data gist-syntax">
             <div class="gist-highlight">
  <pre><div class="line" id="LC3"><span class="p">(</span><span
  class="nf">sqr</span> <span class="mi">0</span><span
  class="p">)</span></div><div class="line" id="LC4"><span
  class="c1">;=&gt; 0</span></div></pre>
             </div>
         </div>
       </div>
  </div>
  In this case, core.contracts provides the provide-contracts macro to
  define contracts and apply them dynamically to existing functions:
  <div class="gist">
       <div class="gist-file">
          <div class="gist-data gist-syntax">
             <div class="gist-highlight">
  <pre><div class="line" id="LC1"><span class="p">(</span><span
  class="nf">provide-contracts</span> </div><div class="line"
  id="LC2">&nbsp;&nbsp;<span class="p">[</span><span
  class="nv">sqr</span> <span class="s">"Constraints for
  squaring"</span> </div><div class="line"
  id="LC3">&nbsp;&nbsp;&nbsp;&nbsp;<span class="p">[</span><span
  class="nv">x</span><span class="p">]</span> <span
  class="p">[</span><span class="nv">number?</span> <span
  class="p">(</span><span class="nb">not= </span><span
  class="mi">0</span> <span class="nv">x</span><span class="p">)</span>
  <span class="nv">=&gt;</span> <span class="nv">number?</span> <span
  class="nv">pos?</span><span class="p">]])</span></div><div
  class="line" id="LC4"><br/></div><div class="line" id="LC5"><span
  class="p">(</span><span class="nf">sqr</span> <span
  class="mi">0</span><span class="p">)</span></div><div class="line"
  id="LC6"><span class="c1">; java.lang.AssertionError:
  </span></div><div class="line" id="LC7"><span class="c1">;   Assert
  failed: (not= 0 n)</span></div></pre>
             </div>
         </div>
       </div>
  </div>
  As shown, the sqr function is dynamically modified with the contract
  defined in the body of provide-contracts.  This macro can take any
  number of vectors where each corresponds to a contract for a given
  function; including multiple arities embedded within.  core.contracts
  also allows you to include existing named contracts (see [defcontract]
  for more information) instead of the contract specification vector, as
  shown below:
  <div class="gist">
       <div class="gist-file">
          <div class="gist-data gist-syntax">
             <div class="gist-highlight">
  <pre><div class="line" id="LC1"><span class="p">(</span><span
  class="nf">defcontract</span> <span
  class="nv">sqr-contract</span></div><div class="line"
  id="LC2">&nbsp;&nbsp;<span class="s">"Defines the constraints on
  squaring."</span></div><div class="line" id="LC3">&nbsp;&nbsp;<span
  class="p">[</span><span class="nv">n</span><span class="p">]</span>
  <span class="p">[</span><span class="nv">number?</span> <span
  class="p">(</span><span class="nb">not= </span><span
  class="mi">0</span> <span class="nv">n</span><span class="p">)</span>
  <span class="nv">=&gt;</span> <span class="nv">pos?</span> <span
  class="nv">number?</span><span class="p">])</span></div><div
  class="line" id="LC4"><br/></div><div class="line" id="LC5"><span
  class="p">(</span><span class="nf">sqr</span> <span
  class="mi">0</span><span class="p">)</span></div><div class="line"
  id="LC6"><span class="c1">;=&gt; 0</span></div><div class="line"
  id="LC7"><br/></div><div class="line" id="LC8"><span
  class="p">(</span><span class="nf">provide-contracts</span></div><div
  class="line" id="LC9">&nbsp;&nbsp;<span class="p">[</span><span
  class="nv">sqr</span> <span class="s">"Apply the contract for
  squaring"</span> </div><div class="line"
  id="LC10">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span
  class="nv">sqr-contract</span><span class="p">])</span></div><div
  class="line" id="LC11"><br/></div><div class="line" id="LC12"><span
  class="p">(</span><span class="nf">sqr</span> <span
  class="mi">0</span><span class="p">)</span></div><div class="line"
  id="LC13"><span class="c1">; java.lang.AssertionError:
  </span></div><div class="line" id="LC14"><span class="c1">;   Assert
  failed: (not= 0 n)</span></div></pre>
             </div>
         </div>
       </div>
  </div>
  provide-contracts gives you a lot of flexibilty in how to separate
  functions from their contracts and likewise apply them in
  domain-specific ways.
  [return to documentation]

  [defconstrainedfn]: ../defconstrainedfn/
  [defcontract]: ./defcontract/
  [return to documentation]: ../docs.html

