# Resolves symbolic links in production mode
JEKYLL = env JEKYLL_ENV=production jekyll

ifdef BASEURL
BASE = --baseurl /~cs232/archive/$(BASEURL)/www
else
BASE = ""
endif

serve:
	bundle exec $(JEKYLL) serve --trace

remote: 
	rm -rf _remote
	$(JEKYLL) build --destination _remote $(BASE) --trace
	chmod -R ugo+rX _remote
	rm _remote/Makefile
	#rm -rf _remote/tools/math_review/solutions

rsync: remote
	rsync -arvz --delete _remote/* cs232@cs.wellesley.edu:current

# To run with remote one should run "make archive BASEURL=s24" to archive to s24, for example
archive: remote
	ssh cs232@cs.wellesley.edu "mkdir -p archive/$(BASEURL)/www"
	rsync -arvz --delete _remote/* cs232@cs.wellesley.edu:archive/$(BASEURL)/www
