# Git Assignment

**INDIVIDUAL ASSIGNMENT**

**Submitter:** Stephen White

**Deadline**: September 18

**Submission Type**: Markdown File on BBLearn

**Value**: Part of in-class/short assignments grade

## Description

### Understanding the repo
1. Download [handson.zip](handson.zip) and unzip it. handson is a git repository. Using the commandline change the directory to "handson/"

2. Draw a diagram of the commits and branches in repository.

    - Use `git branch` to list the branches in this repository.
    - Use `git checkout` to explore each branch.
    - Use `git log --decorate` to explore the structure of commits.

    ```
    $ git branch
           feature-foo
           * master
   ```
   ```

      $ git log --decorate
            commit f67f266cf420735187053f10d32e2c0f7cbc5a43
            Author: Igor Steinmacher <igorsteinmacher@gmail.com>
            Date:   Fri Aug 24 15:30:05 2018 -0700

               Adding class B skeleton

            commit 309b0d73ff9c2163591c9e96e307fe61b4c8f58a
            Author: Igor Steinmacher <igorsteinmacher@gmail.com>
            Date:   Fri Aug 24 15:27:16 2018 -0700

               Adding class A skeleton

            commit 9c1eeb8901b0926ce7fa13cc6ce0a1876fc4179b
            Author: Igor Steinmacher <igorsteinmacher@gmail.com>
            Date:   Fri Aug 24 15:26:44 2018 -0700

               Creating all files (all empty)
    ```

3. Try `git log --graph --all` to see the commit tree
   ```
   $ git log --graph --all

      * commit a70a8e9d3c5390e367028faf033f2a9ef03d2e91
      | Author: Igor Steinmacher <igorsteinmacher@gmail.com>
      | Date:   Fri Aug 24 15:29:22 2018 -0700
      |
      |     Adding header of method foo()
      |
      | * commit f67f266cf420735187053f10d32e2c0f7cbc5a43
      |/  Author: Igor Steinmacher <igorsteinmacher@gmail.com>
      |   Date:   Fri Aug 24 15:30:05 2018 -0700
      |
      |       Adding class B skeleton
      |
      * commit 309b0d73ff9c2163591c9e96e307fe61b4c8f58a
      | Author: Igor Steinmacher <igorsteinmacher@gmail.com>
      | Date:   Fri Aug 24 15:27:16 2018 -0700
      |
      |     Adding class A skeleton
      |
      * commit 9c1eeb8901b0926ce7fa13cc6ce0a1876fc4179b
        Author: Igor Steinmacher <igorsteinmacher@gmail.com>
        Date:   Fri Aug 24 15:26:44 2018 -0700

            Creating all files (all empty)
   ```

4. Use `git diff BRANCH_NAME` to view the differences from a branch and the current branch.
   Summarize the difference from master to the other branch.

    ```
    $ git diff feature-foo
         diff --git a/A.java b/A.java
         index 674b8ce..3ea227e 100755
         --- a/A.java
         +++ b/A.java
         @@ -1,7 +1,4 @@
         public class A {
            -
            -   public void foo() {
            -
            -   }
            +

            }

            diff --git a/B.java b/B.java
            index e69de29..ae64e6b 100755
            --- a/B.java
            +++ b/B.java
            @@ -0,0 +1,4 @@
            +public class B {
            +
            +
            +}
    ```

5. Write a command sequence to merge the non-master branch into `master`

    ***While on master...***
    ```
    $ git merge feature-foo
         Auto-merging A.java
         Merge made by the 'recursive' strategy.
            A.java | 5 ++++-
            1 file changed, 4 insertions(+), 1 deletion(-)
    ```

6. Write a command (or sequence) to (i) create a new branch called `feature-bar` (from the `master`) and (ii) change to this branch

    ***From Master...***
    ```
    $ git checkout -b feature-bar
         Switched to a new branch 'feature-bar'
    ```

7. Edit B.java adding the following source code inside class B:
   ```
   public void bar(){

   }
   ```

   ***Class B now looks as follows on 'feature-bar':***
   ```
   public class B {

      public void bar(){

      }
   }
   ```

8. Write a command (or sequence) to commit your changes
   ```
      $ git add B.java

      $ git commit
            [feature-bar 8607b07] Updating Class B For Question 8
            1 file changed, 2 insertions(+)
   ```

9. Change back to the `master` branch and change B.java adding the following source code (commit your change to `master`):
   ```
   public static void main(){
      System.out.println("Hi")
   }
   ```
   ```
   $ git checkout master
         Switched to branch 'master'
   ```
   ***Class B now looks as follows on 'master':***
   ```
   public class B {

      public static void main(){
         System.out.println("Hi");
      }
   }
   ```
   ```
   $ git add B.java

   $ git commit
         [master 5c75682] Making Changes to B.java for Question 9
         1 file changed, 3 insertions(+), 1 deletion(-)
   ```

10. Write a command sequence to merge the `feature-bar` branch into `master`
   ```
   $ git merge feature-bar
         Auto-merging B.java
         CONFLICT (content): Merge conflict in B.java
         Automatic merge failed; fix conflicts and then commit the result.
   ```

11. What happened?
   ```
   A merge conflict occurred because the same lines of code were altered
   on separate branches, and git does not know which one to choose.
   ```

12. Write a set of commands to abort the merge
   ```
   $ git merge --abort

   $ git status
         On branch master
         nothing to commit, working directory clean
   ```

13. Now repeat item 10, but proceed with the manual merge (Editing B.java). All implemented methods are needed. Explain your procedure

   ***Attempting once more to merge into master...***
   ```
   $ git merge feature-bar
         Auto-merging B.java
         CONFLICT (content): Merge conflict in B.java
         Automatic merge failed; fix conflicts and then commit the result.
   ```
   ***Class B now appears as follows:***
   ```
   public class B {

   <<<<<<< HEAD
      public static void main(){
         System.out.println("Hi");
   =======
      public void bar(){

   >>>>>>> feature-bar
      }
   }
   ```
   ***Upon editing the code, Class B now looks like this:***
   ```
   public class B {

      public static void main(){
         System.out.println("Hi");
      }

      public void bar(){

      }
   }
   ```


14. Write a command (or set of commands) to proceed with the merge and make `master` branch up-to-date

   ***Viewing the status of the branch...***
   ```
   $ git status
         On branch master
         You have unmerged paths.
            (fix conflicts and run "git commit")

         Unmerged paths:
            (use "git add <file>..." to mark resolution)

               both modified:      B.java

         no changes added to commit (use "git add" and/or "git commit -a")
   ```
   ***Proceeding with successful merge...***
   ```
   $ git add B.java
   ```
   ```
   $ git status
         On branch master
         All conflicts fixed but you are still merging.
            (use "git commit" to conclude merge)

         Changes to be committed:

            modified:   B.java
   ```
   ```
   $ git commit
         [master 1865dda] Merge branch 'feature-bar'
   ```
   ***Inspection of the branches displays the following output...***
   ```
   $ git lg
   
         *   1865dda - (HEAD, master) Merge branch 'feature-bar' (33 seconds ago) <Stephen White>
         |\
         | * 8607b07 - (feature-bar) Updating Class B For Question 8 (50 minutes ago) <Stephen White>
         * | 5c75682 - Making Changes to B.java for Question 9 (30 minutes ago) <Stephen White>
         |/
         *   9f37079 - Merge branch 'feature-foo' (66 minutes ago) <Stephen White>
         |
         | * a70a8e9 - Adding header of method foo() (6 days ago) <Igor Steinmacher>
         * f67f266 - Adding class B skeleton (6 days ago) <Igor Steinmacher>
         |
         * 309b0d7 - Adding class A skeleton (6 days ago) <Igor Steinmacher>
         * 9c1eeb8 - Creating all files (all empty) (6 days ago) <Igor Steinmacher>
   ```
   ***Merge was successful!***
